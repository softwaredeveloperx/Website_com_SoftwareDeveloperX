---
ref: Github_Action_file_yml__for_multi_Tenant_with_file_Target_txt
judul: 'Github Action file .yml for multi Tenant with file Target.txt'
title: 'Github Action file .yml for multi Tenant with file Target.txt'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# Github Action file .yml for multi Tenant with file Target.txt

> **note:** this article is a continuation of
> [Infrastructure {Server, CI/ CD, multi Tenant}}](/en/Infrastructure__Server_CI_CD__multi_Tenant/)

## Situation

I have a system {Product} with several Tenants:

- Tenant 1
- Tenant A
- Tenant X
- ...
- Tenant n

each Tenant:

- has a different `DEPLOY_PATH` on the server
- has a different `SERVICE_NAME`
- has a different configuration {`app-settings`}

**Problem:**

I want to perform Deployment in a way that is:

- `consistent` — for all Tenants
- `flexible` — able to choose the target Tenant
- `simple` — no need for many different workflow files

**What-if: no mechanism like this exists?**

- create 1 workflow file per Tenant → many files, hard to maintain
- hardcode target in workflow → need to edit `.yml` file every time you deploy
- human error: accidentally deploying to the wrong Tenant

## Solution: Target.txt file

**Main idea:**

- 1 `.yml` file for all Tenants
- deployment target is determined by the `__Deploy/Target.txt` file
- simply change the content of `Target.txt`, then `git push`
- workflow reads `Target.txt` → deploys to the correct Tenant

**`app-settings.json` file for UI** {externalized configuration}

I want to have a dynamic UI that can connect to a BackEnd, by means of:

- `app-settings.json` file at the _root_
- this file must not be _included_ in the build
- UI will fetch this file
- this file contains the URL end-point of the BackEnd
- UI will connect to that URL

```
__Deploy/
    Target.txt
    app-settings.json
    app-settings--env_dev.json
    app-settings--env_test.json
    app-settings--Tenant_1.json
    app-settings--Tenant_A.json
    app-settings--Tenant_X.json
```

**`Target.txt` format:**

```
tenant1.SoftwareDevelopeRx.com
tenantA.SoftwareDevelopeRx.com
tenantX.SoftwareDevelopeRx.com
```

first line = deployment target

```
tenant1.SoftwareDevelopeRx.com
dotnet_restore
```

second line = optional flag {example: `dotnet_restore`}

**Special value:**

```
no_deployment
```

if the content of `Target.txt` is `no_deployment`:

- workflow still runs
- but does **not** perform deployment
- only `git push`
- _use case_: update documentation, update non-deployment configuration

## Component: Github Action files .yml

I have 4 workflow files:

| File                          | Trigger Branch | Function                             |
| ----------------------------- | -------------- | ------------------------------------ |
| `deploy_framework_engine.yml` | master         | Deploy BackEnd → Framework Engine    |
| `deploy_app_engine.yml`       | master         | Deploy BackEnd → App Engine {plugin} |
| `deploy_framework_UI.yml`     | main           | Deploy FrontEnd → Framework UI       |
| `deploy_app_UI.yml`           | main           | Deploy FrontEnd → App UI             |

> **Note:** BackEnd uses branch `master`, FrontEnd uses branch `main`

## Anatomy: workflow file

every workflow file has a consistent structure:

```
1. Read deployment target   ← read Target.txt
2. Set deployment variables ← mapping target → variables
3. [optional] dotnet restore
4. Build / Publish
5. Deploy application       ← stop service → copy files → start service
```

### Step 1: Read deployment target

```yaml
- name: Read deployment target
  id: read-target
  run: |
      if [ ! -f "__Deploy/Target.txt" ]; then
        echo "Error: __Deploy/Target.txt not found!"
        exit 1
      fi

      # Read first line only
      TARGET=$(head -n 1 __Deploy/Target.txt | tr -d '[:space:]')

      if [ -z "$TARGET" ]; then
        echo "Error: Target is empty!"
        exit 1
      fi

      echo "TARGET=$TARGET" >> $GITHUB_OUTPUT
      echo "📍 Deployment target: $TARGET"
```

validation:

- `Target.txt` file must exist
- first line must not be empty
- trim whitespace — to avoid _human error_ {hidden spaces}

### Step 2: Set deployment variables

```yaml
- name: Set deployment variables
  run: |
      TARGET="${{ steps.read-target.outputs.TARGET }}"

      case "$TARGET" in
        tenantX.SoftwareDevelopeRx.com)
          echo "SERVICE_NAME=Product_Tenant_X"     >> $GITHUB_ENV
          echo "DEPLOY_PATH=/var/www-custom/..."  >> $GITHUB_ENV
          ;;
        no_deployment)
          echo "SHOULD_DEPLOY=false" >> $GITHUB_ENV
          ;;
        *)
          echo "Error: Invalid target '$TARGET'"
          exit 1
          ;;
      esac
```

this pattern:

- `case` statement → mapping from domain to variables
- `GITHUB_ENV` → variables available to all subsequent steps
- `no_deployment` → skip deployment, no error
- `*` → catch invalid target → **fail fast**, not silent

### Step 3: dotnet restore {optional}

specifically for BackEnd Engine:

```yaml
# Read second line for dotnet_restore flag
RESTORE=$(sed -n '2p' __Deploy/Target.txt | tr -d '[:space:]')
if [ "$RESTORE" == "dotnet_restore" ]; then
echo "SHOULD_RESTORE=true" >> $GITHUB_OUTPUT
fi
```

```yaml
- name: Restore packages
  if: env.SHOULD_DEPLOY == 'true' && steps.read-target.outputs.SHOULD_RESTORE == 'true'
  run: dotnet restore --verbosity minimal
```

why optional?

- `dotnet restore` takes time
- if packages have not changed → skip restore → faster deployment
- simply add the second line `dotnet_restore` in `Target.txt` when needed

### Step 4: Build & Publish {BackEnd}

```yaml
- name: Build application
  if: env.SHOULD_DEPLOY == 'true'
  run: |
      dotnet build \
        --configuration Release \
        --verbosity minimal \
        -p:UseSharedCompilation=true \
        -p:BuildInParallel=true

- name: Publish application
  if: env.SHOULD_DEPLOY == 'true'
  run: |
      dotnet publish \
        --configuration Release \
        --no-build \
        --output ./publish-cache \
        --verbosity minimal
```

`--no-build` on publish → does not rebuild, since it was already built in the previous step

### Step 5: Deploy application

**BackEnd {Engine}:**

```yaml
- name: Deploy application
  if: env.SHOULD_DEPLOY == 'true'
  run: |
      # Stop service gracefully
      sudo systemctl stop ${{ env.SERVICE_NAME }} || true
      sleep 2

      # Copy published files
      sudo cp -rf ./publish-cache/* "${{ env.DEPLOY_PATH }}/"

      # Fix ownership
      sudo chown -R nginx:nginx ${{ env.DEPLOY_PATH }}
      sudo chmod -R 755 ${{ env.DEPLOY_PATH }}

      # Start service
      sudo systemctl daemon-reload
      sudo systemctl enable ${{ env.SERVICE_NAME }}
      sudo systemctl start ${{ env.SERVICE_NAME }}

      # Verify service started
      sleep 3
      if ! sudo systemctl is-active --quiet ${{ env.SERVICE_NAME }}; then
        echo "❌ Service failed to start"
        sudo journalctl -u ${{ env.SERVICE_NAME }} --no-pager -n 10
        exit 1
      fi

      echo "✅ Deployment completed successfully!"
```

**FrontEnd {UI}:**

```yaml
- name: Deploy application
  if: env.SHOULD_DEPLOY == 'true'
  run: |
      # Copy all files (excluding .git and __Deploy folder)
      sudo rsync -av --exclude='.git' --exclude='__Deploy' ./ ${{ env.DEPLOY_PATH }}/

      # Fix ownership
      sudo chown -R nginx:nginx ${{ env.DEPLOY_PATH }}
      sudo chmod -R 755 ${{ env.DEPLOY_PATH }}

      echo "✅ Deployment completed successfully!"
```

difference between BackEnd vs FrontEnd:

- BackEnd → stop service → deploy → start service {because there is a running `.dll`}
- FrontEnd → copy files directly {static files, no service restart needed}

## Concurrency: one deployment at a time

```yaml
concurrency:
    group: deploy-app-engine
    cancel-in-progress: false
```

`cancel-in-progress: false` → a deployment that is already running is **not** cancelled by the next push

- _use case_: push to `master` twice in a row → first deployment finishes first, then the second one runs

## Special case: App Engine with DLL copy

```yaml
# Copy DLL to Framework Engine folder
sudo cp -f ${{ env.DEPLOY_PATH }}/APP-Engine.dll ${{ env.COPY_PATH }}/
sudo chown nginx:nginx ${{ env.COPY_PATH }}/APP-Engine.dll
sudo chmod 755 ${{ env.COPY_PATH }}/APP-Engine.dll
```

why is this step needed?

- App Engine {plugin} is loaded by Framework Engine
- after deploying App Engine → copy `.dll` to the Framework Engine folder
- Framework Engine will use the new `.dll` on next restart

## Workflow: how to deploy to a specific Tenant

```
1. edit file __Deploy/Target.txt
   → write the domain of the Tenant to deploy to

2. git add __Deploy/Target.txt
   git commit -m "deploy: Tenant X"
   git push

3. Github Action runs automatically
   → reads Target.txt
   → deploys to the correct Tenant
```

if you only want to `git push` without deployment:

```
1. edit __Deploy/Target.txt → fill in: no_deployment
2. git push
```

## Notes

- `self-hosted` runner → workflow runs on your own server, not on Github's server
- `actions/checkout@v4` with `clean: true` → workspace is always clean before deploy
- `|| true` on `systemctl stop` → no error if service is not yet running {_first time deploy_}
- permission fix on `github.workspace` → for cleanup purposes by the Github runner
