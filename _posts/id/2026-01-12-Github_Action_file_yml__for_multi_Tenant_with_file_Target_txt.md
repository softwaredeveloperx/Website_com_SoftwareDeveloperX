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

> **catatan:** tulisan ini adalah lanjutan dari artikel
> [Infrastructure {Server, CI/ CD, multi Tenant}}](/id/Infrastructure__Server_CI_CD__multi_Tenant/)

## Situasi

saya mempunyai system {Product} dengan beberapa Tenant:

- Tenant 1
- Tenant A
- Tenant X
- ...
- Tenant n

masing-masing Tenant:

- mempunyai `DEPLOY_PATH` yang berbeda di server
- mempunyai `SERVICE_NAME` yang berbeda
- mempunyai konfigurasi {`app-settings`} yang berbeda

**Problem:**

saya ingin melakukan Deployment dengan cara yang:

- `konsisten` — untuk semua Tenant
- `fleksibel` — bisa memilih Tenant target
- `simple` — tidak perlu banyak workflow file yang berbeda

**What-if: tidak ada mekanisme seperti ini?**

- buat 1 workflow file per Tenant → banyak file, susah di-maintain
- hardcode target di workflow → perlu edit file `.yml` setiap kali deploy
- human error: salah deploy ke Tenant yang salah

## Solusi: file Target.txt

**Ide utama:**

- 1 file `.yml` untuk semua Tenant
- target deployment ditentukan oleh file `__Deploy/Target.txt`
- cukup ubah isi `Target.txt`, lalu `git push`
- workflow membaca `Target.txt` → deploy ke Tenant yang tepat

**File `app-settings.json` untuk UI** {externalized configuration}

Saya ingin mempunyai UI yang dynamic yang bisa melakukan koneksi ke suatu BackEnd, dengan cara:

- file `app-settings.json` pada _root_
- file ini tidak boleh _included_ ke dalam build
- UI akan fetch file ini
- file ini berisi informasi URL end-point of BackEnd
- UI akan koneksi ke URL tersebut

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

**Format `Target.txt`:**

```
tenant1.SoftwareDevelopeRx.com
tenantA.SoftwareDevelopeRx.com
tenantX.SoftwareDevelopeRx.com
```

baris pertama = target deployment

```
tenant1.SoftwareDevelopeRx.com
dotnet_restore
```

baris kedua = optional flag {contoh: `dotnet_restore`}

**Special value:**

```
no_deployment
```

jika isi `Target.txt` adalah `no_deployment`:

- workflow tetap berjalan
- tetapi **tidak** melakukan deployment
- hanya `git push` saja
- _use case_: update dokumentasi, update konfigurasi non-deployment

## Component: Github Action files .yml

saya mempunyai 4 workflow files:

| File                          | Trigger Branch | Fungsi                               |
| ----------------------------- | -------------- | ------------------------------------ |
| `deploy_framework_engine.yml` | master         | Deploy BackEnd → Framework Engine    |
| `deploy_app_engine.yml`       | master         | Deploy BackEnd → App Engine {plugin} |
| `deploy_framework_UI.yml`     | main           | Deploy FrontEnd → Framework UI       |
| `deploy_app_UI.yml`           | main           | Deploy FrontEnd → App UI             |

> **Note:** BackEnd menggunakan branch `master`, FrontEnd menggunakan branch `main`

## Anatomy: workflow file

setiap workflow file mempunyai struktur yang konsisten:

```
1. Read deployment target   ← baca Target.txt
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

- file `Target.txt` harus ada
- baris pertama tidak boleh kosong
- trim whitespace — untuk menghindari _human error_ {spasi tersembunyi}

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

pattern ini:

- `case` statement → mapping dari domain ke variables
- `GITHUB_ENV` → variables tersedia untuk semua step berikutnya
- `no_deployment` → skip deployment, tidak error
- `*` → catch invalid target → **fail fast**, tidak silent

### Step 3: dotnet restore {optional}

khusus untuk BackEnd Engine:

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

mengapa optional?

- `dotnet restore` membutuhkan waktu
- jika packages tidak berubah → skip restore → deployment lebih cepat
- cukup tambahkan baris kedua `dotnet_restore` di `Target.txt` jika diperlukan

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

`--no-build` pada publish → tidak build ulang, karena sudah di-build pada step sebelumnya

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

perbedaan BackEnd vs FrontEnd:

- BackEnd → stop service → deploy → start service {karena ada `.dll` yang berjalan}
- FrontEnd → langsung copy files {static files, tidak perlu restart service}

## Concurrency: satu deployment dalam satu waktu

```yaml
concurrency:
    group: deploy-app-engine
    cancel-in-progress: false
```

`cancel-in-progress: false` → deployment yang sedang berjalan **tidak** dibatalkan oleh push berikutnya

- _use case_: push ke `master` dua kali berturut-turut → deployment pertama selesai dulu, baru deployment kedua

## Special case: App Engine dengan copy DLL

```yaml
# Copy DLL to Framework Engine folder
sudo cp -f ${{ env.DEPLOY_PATH }}/APP-Engine.dll ${{ env.COPY_PATH }}/
sudo chown nginx:nginx ${{ env.COPY_PATH }}/APP-Engine.dll
sudo chmod 755 ${{ env.COPY_PATH }}/APP-Engine.dll
```

mengapa ada step ini?

- App Engine {plugin} di-load oleh Framework Engine
- setelah deploy App Engine → copy `.dll` ke folder Framework Engine
- Framework Engine akan menggunakan `.dll` yang baru pada restart berikutnya

## Workflow: cara deploy ke Tenant tertentu

```
1. edit file __Deploy/Target.txt
   → tulis domain Tenant yang ingin di-deploy

2. git add __Deploy/Target.txt
   git commit -m "deploy: Tenant X"
   git push

3. Github Action otomatis berjalan
   → baca Target.txt
   → deploy ke Tenant yang tepat
```

jika hanya ingin `git push` tanpa deployment:

```
1. edit __Deploy/Target.txt → isi: no_deployment
2. git push
```

## Catatan

- `self-hosted` runner → workflow berjalan di server sendiri, bukan di Github server
- `actions/checkout@v4` dengan `clean: true` → workspace selalu bersih sebelum deploy
- `|| true` pada `systemctl stop` → tidak error jika service belum berjalan {_first time deploy_}
- permission fix pada `github.workspace` → untuk keperluan cleanup oleh Github runner
