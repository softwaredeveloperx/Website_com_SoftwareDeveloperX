---
ref: E2E__end_to_end_Testing__4_tipe_Testing_Script
judul: 'E2E {end-to-end} Testing: 4 tipe Testing Script'
title: 'E2E {end-to-end} Testing: 4 tipe Testing Script'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# E2E {end-to-end} Testing: 4 tipe Testing Script

Pengalaman saya menggunakan `Playwright` untuk E2E {end-to-end} Testing, saya membagi `Testing Script` menjadi beberapa Tipe:

Tipe 1: simple Form

- walaupun Form tersebut melibatkan lebih dari 50 field
- dan dibuat secara UI/UX dengan beberapa `TAB` yang terpisah
- tetapi jika tidak ada `List of Items/Details`, maka tetapi saja termasuk Tipe ini

Tipe 2: Header - Detail

- tidak ada hubungannya dengan UI/UX dengan beberapa `TAB` yang terpisah
- polanya adalah:
    - ada bagian sebagai Header
    - ada bagian `List of Items/Details`

Tipe 2 x: Header - Detail - X

- pada Baris di `List of Items/Details`
- ada field/column berupa `Autocomplete`
- yang jika diisi, dia akan "effect" ke field/column lainnya
- contoh:
    - Inventory Item yang `Autocomplete`
    - jika diisi, maka FrontEnd akan melakukan beberapa `fetch`

Tipe 3: UI/UX yang cukup complex
_todo_

Tipe 4: Multi-step / Wizard Form

- Symphony beberapa `Automation Script`
- Form yang harus di-submit bertahap — Step 1 → Step 2 → Step 3 → Final submit.

Tipe 4x:

- seperti Tipe 4 di atas
- ada Tipe 3 di dalamnya

## Generator: membuat secara otomatis - `Testing Script`

<img src="/Aa_images/web-softwaredeveloperx-com/Diagrams/Document_Driven_Development.png" />

Seperti gambar di atas, saya bisa membuat Generator untuk Tipe 1, Tipe 2, Tipe 2x, Tipe 4<br/>

- walaupun untuk Tipe 4, agak susah
- karena harus "passing nilai"
- yang dihasilkan dari suatu _Form step m_, ke _Form step n_

setidaknya akan ada beberapa Generator, yaitu:

```
generator__Test_script.mjs
generator__Test_script__items.mjs

generator__Symphony__Test_script.mjs

generator__md_to_excel.mjs
generator__md_to_excel__items.mjs
```

Tipe 3 dan Tipe 4x, saya harus buat `Testing Script` secara Manual.<br/>
Saya fikir, saya bisa pakai teknik:

- sama sekali tidak buat dari 0
- pancing dulu, dengan membuat versi "lebih sederhana"
- sehingga bisa dibuat secara otomatis menggunakan Generator
- baru kemudian custom, karena menyesuaikan UI/UX yang cukup complex
