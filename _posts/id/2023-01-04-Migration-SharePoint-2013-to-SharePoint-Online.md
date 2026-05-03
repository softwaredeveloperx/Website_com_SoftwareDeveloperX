---
ref: Migration-SharePoint-2013-to-SharePoint-Online
judul: Migration SharePoint 2013 to SharePoint Online
title: 'Migrasi SharePoint 2013 ke SharePoint Online - Pengalaman Nyata 2023'
description: 'Pengalaman migrasi SharePoint 2013 on-premise ke SharePoint Online: document migration, farm solutions, SPFx UI, dan patch authentication untuk aplikasi non-SharePoint.'
tags: [sharepoint]
category: SharePoint
category_url: 'sharepoint-id'
---

# Migration SharePoint 2013 to SharePoint Online

Di Januari 2023, saya mendapatkan project `SharePoint 2013 on premise to SharePoint Online {Microsoft 365}`.<br/>
scope:

1. Document migration
2. Custom Application for SharePoint 2013
    - UI inside some `Master Pages`
    - Solution .wsp
    - WebPart
    - Application Page
    - User mapping
3. UI for SharePoint Online
4. Custom Application - non SharePoint
    - Client memiliki _custom application_ {non SharePoint} yang **sangat banyak**. Semua aplikasi tersebut sudah terintegrasi authentication dengan SharePoint 2013 FBA - _Form Based Authentication_
    - _todo_: integrate authentication with Microsoft 365

## 1. Document migration

Client menyimpan document di SharePoint 2013 `on premise`. Total size document cukup besar {untuk ukuran tahun 2023}.
Mereka ingin melakukan migrasi seluruh document ke SharePoint Online {Microsoft 365}.

## 2. Custom Application for SharePoint 2013

Secara garis besar, saya membagi _custom application_ ini dalam 2 kelompok besar:

- farm solutions
    - berupa .wsp yang berisi file .dll, WebPart, Application Page
- non farm solution
    - UI berupa _Master Pages_
    - _Script Editor Web Part_

Sama sekali tidak ada aplikasi yang mempunyai:

- Custom Field
- Custom Content Type
- Custom Event Receiver

## 3. UI for SharePoint Online

Challenge:

- Microsoft sama sekali tidak memberikan sample, cara customize UI untuk SharePoint Online.<br/>
- SharePoint Online tidak memiliki konsep _Master Page_

Solusi:<br/>

- saya jelaskan pada artikel [UI for SharePoint Online with SPFx Extension](/id/UI-for-SharePoint-Online-with-SPFx-Extension)
- hasilnya, tampilan SharePoint Online bisa disesuaikan sepenuhnya sesuai keinginan client.

## 4. Custom Application - non SharePoint

Challenge:

- _custom application_ {non SharePoint} yang **sangat banyak**
- beberapa Vendor memegang _custom application_ tersebut:
    - saya perlu koordinasi dengan mereka
    - tentang detail aplikasi dan timing untuk patching

Action:

- satu per satu aplikasi, dilakukan patch di bagian authentication
- Aplikasi berbasis PHP
- Aplikasi berbasis ASP.NET Web Form
- Aplikasi FrontEnd menggunakan AngularJS

secara teknis, masing-masing aplikasi dilakukan patching seperti berikut:

1. patch Authentication di sisi FrontEnd saja
2. patch Authentication di sisi BackEnd
