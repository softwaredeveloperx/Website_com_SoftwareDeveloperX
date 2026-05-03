---
ref: Tools-untuk-Migrasi-SharePoint-SPMT-develop-custom-tool
judul: 'SharePoint Migration Tools: SPMT + custom tool'
title: 'SharePoint Migration Tools: SPMT + develop custom tool'
description: 'Tools used for SharePoint migration: SPMT and a custom command-line tool to handle documents skipped or failed by SPMT.'
tags: [sharepoint]
category: SharePoint
category_url: 'sharepoint'
---

# SharePoint Migration Tools: SPMT + develop custom tool

For the project [Migration SharePoint 2013 to SharePoint Online](/en/Migration-SharePoint-2013-to-SharePoint-Online/), I used 2 tools:

- SharePoint Migration Tool (SPMT)
- a custom-built tool

Why?

SPMT frequently ran into issues:

- Errors
- Silently skipping certain documents during migration

Example error:
![Error while using SPMT](/Aa_images/web-softwaredeveloperx-com/sharepoint-migration-01.png)

## Custom Tool

The custom tool is a command-line utility that:

- Compares the Folder + File structure between:
    - Source: SharePoint 2013 on-premise
    - Destination: SharePoint Online
- Uploads documents that were skipped by SPMT
