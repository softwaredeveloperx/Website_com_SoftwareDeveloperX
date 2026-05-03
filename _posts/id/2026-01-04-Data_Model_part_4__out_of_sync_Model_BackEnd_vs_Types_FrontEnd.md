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

## Situasi

**out of sync Model {BackEnd} vs Types {FrontEnd}** bisa terjadi, karena:

- proses Add/Update Delete
- pada Model {BackEnd}
- maupun pada FrontEnd

<img src="/Aa_images/web-softwaredeveloperx-com/Diagrams/Data-Model--out_of_sync_BackEnd_vs_FrontEnd.svg" />

## Solusi

### Solusi 1: Request ke AI

`Prompt` seperti berikut:

saya punya A: {fileName.cs}<br/>
saya punya B: {fileName.js}

tolong check B, perbaiki jika ada yang "tidak tepat":

- berdasarkan A

> Pola `Prompt` ini merupakan implementasi dari:  
> [Request: ke AI secara efektif dan efisien](/id/Request_ke_AI_secara_efektif_dan_efisien__Tone_yang_tepat/)

`Guideline`:

- BackEnd - C#
    - sebagai "Source"
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
        - beberapa field tambahan, untuk keperluan UI

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

### Solusi 2: Auto-generated {untuk Angular modern + TypeScript}

> jika kamu menggunakan Angular {terbaru} + TypeScript,
> ada pendekatan lain: **Types di-generate otomatis** dari BackEnd

`Caranya: Via Script, Bukan "Download" Manual`

- Angular **tidak otomatis** download
- harus jalankan script/command
    - secara manual
    - atau di CI/CD pipeline

**Alurnya:**

```
C# API running {localhost atau server}
    ↓
Swagger endpoint tersedia:
https://localhost:5001/swagger/v1/swagger.json
    ↓
Jalankan command di folder Angular:
npx @openapitools/openapi-generator-cli generate \
  -i https://localhost:5001/swagger/v1/swagger.json \
  -g typescript-angular \
  -o ./src/app/generated
    ↓
File TypeScript ter-generate di folder /generated
```

bisa juga ditambahkan ke `package.json`, agar lebih praktis:

```json
"scripts": {
  "generate-api": "openapi-generator-cli generate ..."
}
```

lalu jalankan dengan:

```
npm run generate-api
```

**Catch:**

- "auto-generated" **tidak semudah kedengarannya**
    - tetap butuh trigger: manual atau pipeline
- Naming convention custom {suffix `X`, `W`, `R`, dll} → **tidak ter-generate**
- `[Computed]` / `[JsonIgnore]` fields → bisa bocor ke spec

> dengan kata lain:
> "auto-generated" dan "manual" — **tidak jauh berbeda effort-nya**
> terutama jika perubahan tidak terlalu sering
