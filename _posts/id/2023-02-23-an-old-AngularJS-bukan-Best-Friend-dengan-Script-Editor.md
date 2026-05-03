---
ref: an-old-AngularJS-bukan-Best-Friend-dengan-Script-Editor
judul: an old AngularJS bukan Best Friend dengan Script Editor
title: 'an old AngularJS bukan Best Friend dengan Script Editor'
description: 'Fakta bahwa aplikasi berbasis an old AngularJS tidak bisa di load menggunakan Script Editor'
tags: [sharepoint]
category: SharePoint
category_url: 'sharepoint-id'
---

# an old AngularJS bukan Best Friend dengan Script Editor

Sesuai dengan Project saya di [Migration SharePoint 2013 to SharePoint Online](/id/Migration-SharePoint-2013-to-SharePoint-Online/)<br/>
Client cukup banyak mempunyai aplikasi berbasis AngularJS yang berjalan di atas SharePoint 2013.

## Situasi:

- AngularJS == ok dengan `Script Editor` di SharePoint 2013
- AngularJS dengan `Script Editor` di SharePoint SharePoint
    - running ok untuk Script yang sederhana
    - tidak ok, jika sudah mulai banyak Service

Saya yakin, itu tentang `Timing` seperti saya sudah jelaskan di [Script Editor for SharePoint Online, Tantangan dan Solusi](https://softwaredeveloperx.com/id/Script-Editor-for-SharePoint-Online/), tetapi tetap saja -- saya tidak berhasil membuatnya jalan lancar.

## Solusi:

- Convert aplikasi AngularJS tersebut ke JQuery
- atau Framework yang lain

## At the End:

- saya melakukan konversi beberapa aplikasi berbasis AngularJS ke JQuery
- semua running ok
