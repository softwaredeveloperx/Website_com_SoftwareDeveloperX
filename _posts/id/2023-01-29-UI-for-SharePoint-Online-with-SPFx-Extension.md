---
ref: UI-for-SharePoint-Online-with-SPFx-Extension
judul: UI for SharePoint Online with SPFx Extension
title: 'Custom UI untuk SharePoint Online menggunakan SPFx Extension'
description: 'Cara membuat custom UI di SharePoint Online dengan SPFx Extension untuk override CSS, mengatasi masalah flicker, dan memudahkan perubahan tampilan tanpa redeploy.'
tags: [sharepoint]
category: SharePoint
category_url: 'sharepoint-id'
---

# UI for SharePoint Online

**Challenge:**

- Microsoft tidak memberikan detail guideline + sample, cara customize UI untuk SharePoint Online.<br/>
    - hanya simple _some color_ untuk `Theme` di SharePoint Online
- SharePoint Online tidak memiliki konsep `Master Page` {seperti di SharePoint 2013}

**Solusi:**

- buat _custom_ `Extension` menggunakan _SPFx: SharePoint Framework_
- Extension akan load style .css

Saya membuat 2 kelompok style .css:

1. di dalam Extension tersebut
2. file .css yang ditaruh pada folder di Document Library

**Why ?**

- mengapa tidak cukup 1 tempat saja ?
- mengapa harus di 2 tempat ?

**Because:**

1. Timing + Flicker
2. Easy to modify

**Situation**

> SharePoint Online banyak melakukan load file-file .css

**Solusi yang saya pilih**

> Kita harus melakukan _override_ ke beberapa style milik SharePoint Online.

**Cara implementasi:**

- style .css yang kita gunakan, harus diload pada _Timing_ yang tepat
- jika tidak, maka akan terjadi _Flicker_, seperti berikut:
    - SharePoint Online akan menampilkan Theme asli miliknya {kita bisa ubah nilai Theme ini}
    - biasanya Warna Biru
    - selanjutnya style .css milik kita, yang akan bekerja
    - user akan melihat terjadi _Flicker_ pada layar
- Easy to modify:
    - seringkali, kita memerlukan perubahan CSS -- tanpa harus melakukan proses Develop/Deploy terhadap _custom SFPx_

**Summary**

> Dengan semua teknik di atas, kita akan dengan sangat mudah mempunyai UI yang sesuai dengan keinginan user, terintegrasi dengan SharePoint Online
