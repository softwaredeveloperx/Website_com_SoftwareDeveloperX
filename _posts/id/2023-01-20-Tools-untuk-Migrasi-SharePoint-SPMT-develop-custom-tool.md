---
ref: Tools-untuk-Migrasi-SharePoint-SPMT-develop-custom-tool
judul: 'Tools untuk Migrasi SharePoint: SPMT + develop custom tool'
title: 'Tools untuk Migrasi SharePoint: SPMT + develop custom tool'
description: 'Tools untuk Migrasi SharePoint: SPMT + develop custom tool'
tags: [sharepoint]
category: SharePoint
category_url: 'sharepoint-id'
---

# Tools untuk Migrasi SharePoint: SPMT + develop custom tool

Untuk project [Migration SharePoint 2013 to SharePoint Online](/id/Migration-SharePoint-2013-to-SharePoint-Online/), saya menggunakan 2 tool:

- SharePoint Migration Tool (SPMT)
- develop custom tool

Why ?

Seringkali SPMT mengalami kendala:

- Error
- skip melakukan migrasi terhadap suatu Document

contoh error:
![Error while using SPMT](/Aa_images/web-softwaredeveloperx-com/sharepoint-migration-01.png)

## Develop custom tool

Custom tool ini berupa command line:

- compare Folder+File structure
    - soure: SharePoint 2013 on-premise
    - destination: SharePoint Online
- melakukan upload Document {yang diskip oleh SPMT}
