---
ref: Data_Model_part_4__out_of_sync_Model_BackEnd_vs_Types_FrontEnd
judul: 'Data Model part 4 - out of sync Model {BackEnd} vs Types {FrontEnd}'
title: 'Data Model part 4 - out of sync Model {BackEnd} vs Types {FrontEnd}'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# Data Model part 4 - out of sync Model {BackEnd} vs Types {FrontEnd}

## Situation

**out of sync Model {BackEnd} vs Types {FrontEnd}** can happen due to:

- Add / Update / Delete processes
- on the Model {BackEnd}
- as well as on the FrontEnd

<img src="/Aa_images/web-softwaredeveloperx-com/Diagrams/Data-Model--out_of_sync_BackEnd_vs_FrontEnd.svg" />

## Solution

### Solution 1: Request to AI

Use a `Prompt` like the following:

I have A: {fileName.cs}<br/>
I have B: {fileName.js}

please check B, fix anything that is "not correct":

- based on A

> This `Prompt` pattern is an implementation of:  
> [Request: to AI effectively and efficiently](/en/Request_to_AI_effectively_and_efficiently__the_right_Tone/)

`Guideline`:

- BackEnd - C#
    - as the "Source"
- FrontEnd:
    - in General:
        - as is
            - do not use convert become CamelCase or PascalCase or something else
            - use as is
        - default value
            - string: ''
            - number: 0
            - boolean: false
            - Date: null
    - Specific on technical:
        - plain JavaScript
            - const
            - spread operator {for Class Inheritance}
        - an old AngularJS
            - avoid const
            - in term of Service
        - some additional fields, for UI purposes

```js
'use strict'

angular.module('app.ourUtils').factory('T_TypeName', [
    function () {
        var service = {}

        service.Something = {
            Code: '',
            abc: 0,
            // ...: ...
        }

        return service
    },
])
```

---

### Solution 2: Auto-generated {for modern Angular + TypeScript}

> if you are using Angular {latest} + TypeScript,
> there is another approach: **Types are auto-generated** from the BackEnd

`How: Via Script, Not Manual "Download"`

- Angular does **not automatically** download
- you need to run a script/command
    - manually
    - or in a CI/CD pipeline

**The flow:**

```
C# API running {localhost or server}
    ↓
Swagger endpoint available:
https://localhost:5001/swagger/v1/swagger.json
    ↓
Run command in the Angular folder:
npx @openapitools/openapi-generator-cli generate \
  -i https://localhost:5001/swagger/v1/swagger.json \
  -g typescript-angular \
  -o ./src/app/generated
    ↓
TypeScript files are generated in the /generated folder
```

you can also add it to `package.json` for convenience:

```json
"scripts": {
  "generate-api": "openapi-generator-cli generate ..."
}
```

then run it with:

```
npm run generate-api
```

**Catch:**

- "auto-generated" is **not as easy as it sounds**
    - still requires a trigger: manual or pipeline
- Custom naming conventions {suffix `X`, `W`, `R`, etc} → **will not be generated**
- `[Computed]` / `[JsonIgnore]` fields → may leak into the spec

> in other words:
> "auto-generated" and "manual" — **are not that different in effort**
> especially if changes are not that frequent
