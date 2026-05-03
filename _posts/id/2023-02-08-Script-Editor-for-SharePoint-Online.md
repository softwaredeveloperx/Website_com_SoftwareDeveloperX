---
ref: Script-Editor-for-SharePoint-Online
judul: Script Editor for SharePoint Online, Tantangan dan Solusi
title: 'Script Editor for SharePoint Online, Tantangan dan Solusi'
description: 'Cara untuk menampilkan script/html/css di SharePoint Online, berserta Challenge dan Solusi'
tags: [sharepoint]
category: SharePoint
category_url: 'sharepoint-id'
---

# Script Editor for SharePoint Online, Tantangan dan Solusi

Saya seringkali mengambil langkah yang pragmatis ([the Pragmatic Programmer](https://en.wikipedia.org/wiki/The_Pragmatic_Programmer)), dengan fokus:

1. Solve the problem
2. not Perfectionist
    - hindari `Over Engineering`
    - Good > Perfect
    - Shipment {Delivery} the Result {tulisan, `Code`, ...}

Refleks yang sama, terbawa untuk urusan custom Application di atas platform SharePoint Online.<br/>
SPFx is very good, tetapi untuk simple script ? no thanks.

- prepare SPFx
- React dan segala macam dependency
- semuanya sekitar 600 MB

## My journey:

- SharePoint 2010/2013
    - Server Side: [WebPart to load .ascx file in SharePoint WSS 3 / MOSS 2007](/id/WebPart-to-load-ascx-file-in-SharePoint-WSS-3-MOSS-2007/)
    - Client Side: Script Editor {standard dari SharePoint}
- SharePoint Online
    - Script editor web part for modern pages [react-script-editor](https://github.com/pnp/sp-dev-fx-webparts/tree/main/samples/react-script-editor)<br/>

> saya fikir, nama `react-script-editor` kurang tepat.
> User berfikir bahwa ini untuk melakukan load terhadap `React Script`, padahal ini adalah WebPart untuk load script/html/css
> dan WebPart ini dibuat menggunakan `React`

## My favourite for custom app on SharePoint Online:

1. develop SPFx Extension for UI/Theme
2. JavaScript/HTML/CSS loaded by `react-script-editor`
3. jika nomor 2 ada kendala {biasanya masalah `get Token` di SharePoint Online}<br/>
   then: develop SPFx WebPart

## Challenge

1. seperti biasa: masalah `Timing` pada script JavaScript
    - terutama sering terjadi pada Aplikasi yang memerlukan module yang lain
    - ini bisa dimengerti, bila merujuk pada _Internal - how `react-script-editor` works_
2. Page Load
    - di SharePoint Online, perpindahan antar 1 page ke page lain, seringkali tidak membuat Page tersebut di load ulang
        - mungkin itu memang nature - di SharePoint Online
        - mungkin itu memang umum, di semua WebPage zaman sekarang
        - saya tidak terlalu paham
    - akibanya: logic aplikasi kita menjadi kacau

## Solusi

- aware terhadap Situasi _Timing_ di atas
- bisa dihandle dengan cara check Flag/Kondisi
