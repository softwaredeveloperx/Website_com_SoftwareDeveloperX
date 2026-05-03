---
ref: Me-and-SharePoint
judul: Me and SharePoint {2007, 2010, 2013 and SharePoint Online}
title: 'My Journey with Microsoft SharePoint - 2007 to 2024'
description: 'My experience as a SharePoint developer since WSS 3/MOSS 2007, Livelink DMS migration, SharePoint 2010, 2013, through SharePoint Online and SPFx in 2024.'
tags: [sharepoint]
category: SharePoint
category_url: 'sharepoint'
---

# Me and SharePoint {2007, 2010, 2013 and SharePoint Online}

My journey with Microsoft SharePoint started back in 2007:

- WSS Service 3 {Windows SharePoint Services version 3.0}
- SharePoint 2007 {MOSS}

I was lucky, because back in 2007 I was already able to build:

- SharePoint Page --> access SAP data
- show data
- execute ZBAPI

Details in the article [WebPart to load .ascx file in SharePoint WSS 3 / MOSS 2007](/en/WebPart-to-load-ascx-file-in-SharePoint-WSS-3-MOSS-2007/)

## 2013 - Migrate Livelink DMS to SharePoint 2010

I was involved in a project to migrate documents from Livelink DMS {Document Management System} to SharePoint 2010.<br/>
About Livelink DMS:

- a _Web Application_ running on IIS Web Server
- Oracle Database

Tool: Avepoint SharePoint migration

The project involved teams from several countries:

- Indonesia
- UK
- Vietnam
- Avepoint team {Singapore, Canada}

A valuable experience from this project — it was the first time I worked with a team across multiple countries.

Each team migrated content from their respective country.<br/>
We held regular online meetings for sharing sessions.

Challenge:

- The Avepoint tool we used frequently threw errors
- We had meetings with Avepoint Singapore, then escalated to Avepoint Canada
- Still not resolved
- I eventually discovered that the errors occurred because the IIS Web Server became `hung` due to the enormous number of requests from the Avepoint tool<br/>
  {while the Oracle Database was perfectly fine}.

Solution:

- In IIS, I created 3 _Web Applications_, each with its own _App Pool_
- All connected to the same Oracle Database
    - Livelink web 1
    - Livelink web 2
    - Livelink web 3
- Avepoint tool then migrated as follows:
    - Finance folder, from _Livelink web 1_
    - SCM folder, from _Livelink web 2_
    - Other folders, from _Livelink web 3_

## 2017 - Migrate SharePoint 2010 to SharePoint 2013

This project was relatively straightforward — it only required a backup/restore of the SharePoint Database {from SharePoint 2010 to SharePoint 2013}.

## 2022 - Migrate SharePoint 2013 to SharePoint Online

At my workplace, a decision was made to migrate from SharePoint 2013 to SharePoint Online. The project involved teams from several countries:

- Indonesia
- UK
- Vietnam
- America, as Project Management consultant

## 2023 - Migrate SharePoint 2013 to SharePoint Online

In January 2023, I personally handled the project [Migration SharePoint 2013 to SharePoint Online](/en/Migration-SharePoint-2013-to-SharePoint-Online/)

## 2024 - Custom SPFx on SharePoint Online

In October 2024, I worked on a project building Custom SPFx on SharePoint Online.<br/>
The UI technique for SharePoint Online is explained in: [UI for SharePoint Online with SPFx Extension](/en/UI-for-SharePoint-Online-with-SPFx-Extension/)<br/>

As a result, the client got a SharePoint Online UI that fully matched their brand.
