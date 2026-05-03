---
ref: 2023-01-28-WebPart-to-load-ascx-file-in-SharePoint-WSS-3-MOSS-2007
judul: WebPart to load .ascx file in SharePoint WSS 3 / MOSS 2007
title: 'WebPart to Load .ascx File in SharePoint WSS 3 / MOSS 2007'
description: 'A technique for building a custom WebPart in SharePoint WSS 3 / MOSS 2007 that loads .ascx files without restarting IIS, including integration with SAP .NET Connector.'
tags: [sharepoint]
category: SharePoint
category_url: 'sharepoint'
---

# WebPart to load .ascx file in SharePoint WSS 3 / MOSS 2007

Back in 2007, building a `custom .wsp` on top of SharePoint WSS 3 / MOSS 2007 was quite challenging:

- WSS 3 / MOSS 2007 is an _ASP.NET Web Application_ running on IIS Web Server
- every deployment of a _custom .wsp_ would trigger an IIS Web Server `restart`
- _take a long time_

## WebPart to load .ascx

I found a WebPart on the Internet {I forget its name} with one core idea:

- load a .ascx text file

The workflow was:

- create a `WebPart Page` in SharePoint
- go to Page Settings, then add the WebPart to the page
- in WebPart Settings, select the .ascx file to load

## Create my own

The approach was so simple that I decided to build my own version.<br/>
Why?

- The original WebPart {from the Internet} had a Folder Setting:
    - it displayed a Dropdown listing all .ascx files in that folder
    - for some reason, every time it rendered the Dropdown, it was _take a long time_
    - possibly because it compiled/built all .ascx files in the folder
- Mine:
    - simply accepts a Textbox for the `path` of the .ascx file
    - loads that _path .ascx file_

## `Code Behind` technique

A .ascx file works just like a .aspx file — it supports the _Code Behind_ technique.<br/>
Combined with `Import` for several `Namespace` declarations inside the .ascx file, it feels like coding `Classic ASP or PHP` on top of the SharePoint platform.<br/>
Why?

- very simple — everything is just .ascx text files
- no Compile step<br/>
  {ASP.NET will compile .aspx/.ascx text files automatically on first _load_.}
- no need to deploy or restart IIS Web Server

## SAP .NET Connector

Around that time, SAP released SAP.NET Connector version 3, which allowed .NET-based applications to access SAP data.<br/>
Combining:

- WebPart loading a .ascx text file
- .ascx text file
- _Code Behind_
- `Import` for several `Namespace`

Result:

- SharePoint Page --> access SAP data
- show data
- execute `ZBAPI`
