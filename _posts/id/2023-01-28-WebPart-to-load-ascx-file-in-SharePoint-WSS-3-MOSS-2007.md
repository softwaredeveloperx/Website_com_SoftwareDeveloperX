---
ref: 2023-01-28-WebPart-to-load-ascx-file-in-SharePoint-WSS-3-MOSS-2007
judul: WebPart to load .ascx file in SharePoint WSS 3 / MOSS 2007
title: 'WebPart untuk Load File .ascx di SharePoint WSS 3 / MOSS 2007'
description: 'Teknik membuat custom WebPart di SharePoint WSS 3 / MOSS 2007 yang dapat load file .ascx tanpa restart IIS, termasuk integrasi dengan SAP .NET Connector.'
tags: [sharepoint]
category: SharePoint
category_url: 'sharepoint-id'
---

# WebPart to load .ascx file in SharePoint WSS 3 / MOSS 2007

Di tahun 2007, membuat `custom .wsp` di atas platform SharePoint WSS 3 / MOSS 2007 == sangat menantang:

- WSS 3 / MOSS 2007 adalah _ASP.NET Web Application_ yang running di pada IIS Web Server
- setiap kali proses deploy _custom .wsp_, akan menyebabkan `restart` IIS Web Server
- _take a long time_

## WebPart to load .ascx

Saya menggunakan suatu WebPart yang saya download dari Internet {saya lupa nama WebPart tersebut}.<br/>
Ide utama WebPart ini:

- load file text .ascx

Jadi kita bisa menggunakan dengan cara berikut:

- kita buat `WebPart Page` pada SharePoint
- Page Setting, kemudian kita add WebPart ke Page yang baru dibuat
- WebPart Setting, pilih file .ascx yang akan di load

## Create my own

Karena cara kerja yang sangat simple di atas, maka saya memutuskan untuk membuat versi saya sendiri.<br/>
Why ?

- WebPart {dari Internet} tersebut, mempunyai Setting suatu Folder
    - dia akan menampilkan Dropdown - daftar file-file .ascx pada Folder tersebut
    - entah bagaimana ceritanya, setiap kali menampilkan Dropdown - daftar file-file .ascx<br/>
      _take a long time_
    - mungkin dilakukan proses compile/build atau apalah itu, terhadap file-file .ascx di Folder
- Mine:
    - cukup menerima Textbox untuk `path` file .ascx
    - load _path file .ascx_

## teknik `Code Behind`

File .ascx, sama dengan file .aspx, sehingga support teknik _Code Behind_.<br/>
Ditambah dengan `Import` untuk beberapa `Namespace` di dalam file .ascx, maka kita seperti coding `Classic ASP or PHP` di atas platform SharePoint.<br/>
Why ?

- sangat simple, karena semua hanya berupa file-file text .ascx
- tidak ada proses Compile<br/>
  {ASP.NET akan melakukan compile file text .aspx/.ascx saat pertama kali _load_.}
- tidak usah melakukan deploy / restart IIS Web Server

## SAP .NET Connector

Di tahun itu, SAP mengeluarkan SAP.NET Connector versi 3 yang mengizinkan aplikasi berbasis .NET untuk akses data SAP.<br/>
Kombinasi:

- WebPart load file text .ascx
- file text .ascx
- _Code Behind_
- `Import` untuk beberapa `Namespace`

Result:

- SharePoint Page --> akses data SAP
- show data
- execute `ZBAPI`
