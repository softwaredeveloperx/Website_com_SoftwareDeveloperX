---
ref: Document_Driven_Development__Specification_Document__Source_of_Truth
judul: 'Document Driven Development - Specification Document (Source of Truth)'
title: 'Document Driven Development - Specification Document (Source of Truth)'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# Document Driven Development - Specification Document (Source of Truth)

Situasi:

saya mempunyai system yang cukup kompleks, yang sudah saya jelaskan pada artikel [Data Model part 1 - Entity, DTO {Data Transfer Object}](/id/Data_Model_part_1__Entity_DTO_Data_Transfer_Object/)

<img src="/Aa_images/web-softwaredeveloperx-com/Diagrams/Data-Model.svg" />

- data dari suatu bagian ke bagian lain
- data dari suatu Layer ke Layer lainnya
- contoh: View HTML, jangan sampai "link" ke fieldName {Model} yang tidak tepat
- Next:
    - E2E Testing Script {di zaman sekarang, ini _is a must_ (bukan lagi _nice to have_)}
    - sebaiknya Testing Script bisa dibuat menggunakan `Generator`

Objective:
<br/>Saya memerlukan `Source of Truth` sebagai acuan bagi semua Component di system

## .MD File sebagai `Source of Truth` - Specification Document

Saya menggunakan .MD file, karena:

- mudah dibaca
- mudah untuk dilakukan suatu "Marking"
- simple _Text File_
- di GitHub, proses Copy/Page image ke .MD file == sangat mudah

Selanjutnya seperti saya tulis pada artikel [Cara menulis file .MD](/id/Cara-menulis-file-MD/), pada bagian:

Too Few vs Too Much

```
❌ Too Few   → Incomplete, tidak berguna
❌ Too Much  → Overwhelmed, kebanjiran informasi
✅ Pragmatic
```

saya harus menemukan _sweet spot_ -- yang "pas".

maka saya membagi .MD file setidaknya menjadi beberapa kategori:

- Tipe 1: .MD file untuk `Specification Document`:
    - tentang teknis suatu Tool
    - tentang Business Flow yang harus diimplementasikan oleh Code
    - kombinasi keduanya
- Tipe 2: .MD file sebagai input suatu Tool
- Tipe 3: .MD file sebagai User Guide

setidaknya mengurangi _distraction_ bagi pembaca.<br/>
contoh:

- suatu [.MD file untuk `Specification Document`], tidak usah ditulis tentang cara pakai suatu tool
- itu membuat gagal fokus {saya sering mengalami hal ini}

<img src="/Aa_images/web-softwaredeveloperx-com/Diagrams/Document_Driven_Development.png" />

Seperti gambar di atas, semua mengacu pada .MD file {sebagai `Source of Truth` - Specification Document}

- jangan lupa bahwa itu bukan hanya 1 jenis .MD file
- tetapi paling sedikit ada 3 Tipe .MD file, seperti penjelasan di atas

## `Generator` bisa dibuat, karena `Source of Truth` sudah tersedia

setidaknya akan ada beberapa Generator, yaitu:

```
generator__Test_script.mjs
generator__Test_script__items.mjs

generator__md_to_excel.mjs
generator__md_to_excel__items.mjs
```

saya tulis pada artikel [E2E {end-to-end} Testing: 4 tipe Testing Script](/id/E2E__end_to_end_Testing__4_tipe_Testing_Script/) bagian _Generator: membuat secara otomatis - Testing Script_

## WHAT NOT

- Generator - Form / UI

### WHY NOT ?

- daripada membuat `Generator - Form / UI` {karena Form/UI biasanya cukup kompleks}
- lebih baik menggunakan `Request to -- AI`, untuk membuat suatu Form / UI<br/>

contoh: artikel [Request: ke AI secara efektif dan efisien {Tone yang tepat}](/id/Request_ke_AI_secara_efektif_dan_efisien__Tone_yang_tepat/) pada bagian `Case study 1: Request - generate Code dari Gambar`

## Contoh .MD File, untuk Document Driven Development

Saya bahas tentang Contoh .MD File pada [di sini](/id/Contoh_MD_File__Document_Driven_Development/)
