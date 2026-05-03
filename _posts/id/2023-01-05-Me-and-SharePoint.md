---
ref: Me-and-SharePoint
judul: Me and SharePoint {2007, 2010, 2013 and SharePoint Online}
title: 'Perjalanan Saya dengan Microsoft SharePoint - 2007 hingga 2024'
description: 'Sharing pengalaman sebagai SharePoint developer sejak WSS 3/MOSS 2007, migrasi Livelink DMS, SharePoint 2010, 2013, hingga SharePoint Online dan SPFx di 2024.'
tags: [sharepoint]
category: SharePoint
category_url: 'sharepoint-id'
---

# Me and SharePoint {2007, 2010, 2013 and SharePoint Online}

Perjalanan saya dengan Microsoft SharePoint dimulai sejak 2007:

- WSS Service 3 {Windows SharePoint services versi 3.0}
- SharePoint 2007 {MOSS}

Saya sangat beruntung, karena di tahun 2007 sudah bisa membuat:

- SharePoint Page --> akses data SAP
- show data
- execute ZBAPI

Detail pada artikel [WebPart to load .ascx file in SharePoint WSS 3 / MOSS 2007](/id/WebPart-to-load-ascx-file-in-SharePoint-WSS-3-MOSS-2007/)

## 2013 - Migrate Livelink DMS to SharePoint 2010

Saya terlibat project untuk migrasi document yang ada di Livelink DMS {Document Management System} ke SharePoint 2010.<br/>
Teknis tentang Livelink DMS:

- sebuah _Web Application_ berjalan di IIS Web Server
- Database Oracle

Tool: Avepoint SharePoint migration

Project ini melibatkan team dari beberapa negara:

- Indonesia
- UK
- Vietnam
- Team Avepoint {Singapore, Canada}

Pengalaman berharga dari project ini adalah untuk pertama kalinya saya bekerja dengan team dari berbagai negara.

Masing-masing team, melakukan migrasi terhadap content yang ada di negaranya.<br/>
Kami secara berkala melakukan meeting online, untuk sharing session.

Challenge:

- Tool Avepoint yang kami gunakan, sering mengalami error
- kami meeting dengan Avepoint Singapore, yang berikutnya kami meeting dengan Avepoint Canada
- tetap saja: tidak solved
- akhirnya saya tahu, bahwa error terjadi karena IIS Web Server menjadi `hang` karena menerima request yang sangat banyak dari Tool Avepoint<br/>
  {sedangkan Oracle Database baik-baik saja}.

Solusi:

- di IIS, saya membuat 3 _Web Application_ dengan masing-masing _App Pool_ yang berbeda
- semuanya koneksi ke Database Oracle yang sama
    - Livelink web 1
    - Livelink web 2
    - Livelink web 3
- Tool Avepoint melakukan migrasi, sebagai berikut:
    - folder Finance, dari _Livelink web 1_
    - folder SCM, dari _Livelink web 2_
    - folder lainnya, dari _Livelink web 3_

## 2017 - Migrate SharePoint 2010 to SharePoint 2013

Project ini relatif mudah, karena hanya melakukan backup/restore Database SharePoint {dari Database SharePoint 2010 ke Database SharePoint 2013}.

## 2022 - Migrate SharePoint 2013 to SharePoint Online

Di tempat saya bekerja, diputuskan untuk dilakukan migrasi dari SharePoint 2013 ke SharePoint Online. Project ini melibatkan team beberapa negara:

- Indonesia
- UK
- Vietnam
- Amerika, sebagai consultant untuk Project Management

## 2023 - Migrate SharePoint 2013 to SharePoint Online

Di January 2023, saya sendiri menghandle project [Migration SharePoint 2013 to SharePoint Online](/id/Migration-SharePoint-2013-to-SharePoint-Online/)

## 2024 - Custom SPFx di SharePoint Online

Di bulan Oktober 2024, saya bekerja untuk project pembuatan Custom SPFx di SharePoint Online.<br/>
Teknik untuk UI di SharePoint Online, saya jelaskan pada artikel: [UI for SharePoint Online with SPFx Extension](/id/UI-for-SharePoint-Online-with-SPFx-Extension/) <br/>

Hasilnya, client mendapatkan UI SharePoint Online yang sepenuhnya sesuai brand mereka.
