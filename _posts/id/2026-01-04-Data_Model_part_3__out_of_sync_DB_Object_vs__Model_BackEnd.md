---
ref: Data_Model_part_3__out_of_sync_DB_Object_vs__Model_BackEnd
judul: 'Data Model part 3 - out of sync Database Object {Table, View} vs Model {BackEnd}'
title: 'Data Model part 3 - out of sync Database Object {Table, View} vs Model {BackEnd}'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# Data Model part 3 - out of sync Database Object {Table, View} vs Model {BackEnd}

## Situasi

**out of sync Database Object {Table, View} vs Model {BackEnd}** bisa terjadi, karena:

- proses Add/Update Delete
- pada Database Object {Table, View}
- maupun pada Model {BackEnd}

<img src="/Aa_images/web-softwaredeveloperx-com/Diagrams/Data-Model--out_of_sync_DB_Object_vs__Model_BackEnd.svg" />

## Solusi

`Prompt` seperti berikut:

saya punya A: {fileName_DB_Object.sql}<br/>
saya punya B: {fileName.cs}

tolong check B, perbaiki jika ada yang "tidak tepat":

- berdasarkan A

> Pola `Prompt` ini merupakan implementasi dari:  
> [Request: ke AI secara efektif dan efisien](/id/Request_ke_AI_secara_efektif_dan_efisien__Tone_yang_tepat/)

`Guideline`:

- Database Object {Table, View}
- sebagai "Source"

**Contoh kasus: kolom baru di Database, lupa di-update di Model {BackEnd}**

Situasi:

- ada kolom baru: `ApprovalStatus` ditambahkan di `Table` Sales Order
- Model {BackEnd} **tidak diupdate**

Efeknya:

- saat Write data → kolom `ApprovalStatus` selalu `NULL` di Database
- saat Read data → field `ApprovalStatus` tidak ada di response API
- FrontEnd tidak bisa menampilkan data yang seharusnya ada
- bug seperti ini **susah dilacak** — tidak ada error, data hanya "hilang diam-diam"

> _silent bug_ — lebih berbahaya dari error yang jelas

**Kenapa Database Object dijadikan "Source of Truth"?**

- Database adalah _endpoint_ terakhir dari data
- jika Database dan Model tidak sinkron → data yang tersimpan bisa salah, atau data tidak terbaca
- sebaliknya: jika Model yang dijadikan "Source" → risiko _mismatch_ dengan struktur aktual Database

> Database Object = ground truth<br/>
> Model BackEnd = harus mengikuti Database
