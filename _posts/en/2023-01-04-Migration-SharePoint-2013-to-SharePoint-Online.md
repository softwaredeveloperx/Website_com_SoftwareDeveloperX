---
ref: Migration-SharePoint-2013-to-SharePoint-Online
judul: Migration SharePoint 2013 to SharePoint Online
title: 'Migration SharePoint 2013 to SharePoint Online - Real Experience 2023'
description: 'Real experience migrating SharePoint 2013 on-premise to SharePoint Online: document migration, farm solutions, SPFx UI, and authentication patching for non-SharePoint applications.'
tags: [sharepoint]
category: SharePoint
category_url: 'sharepoint'
---

# Migration SharePoint 2013 to SharePoint Online

In January 2023, I handled a project for `SharePoint 2013 on premise to SharePoint Online {Microsoft 365}`.<br/>
Scope:

1. Document migration
2. Custom Application for SharePoint 2013
    - UI inside some `Master Pages`
    - Solution .wsp
    - WebPart
    - Application Page
    - User mapping
3. UI for SharePoint Online
4. Custom Application - non SharePoint
    - The client had **a lot** of _custom applications_ {non SharePoint}. All of them were integrated with SharePoint 2013 FBA - _Form Based Authentication_
    - _todo_: integrate authentication with Microsoft 365

## 1. Document Migration

The client stored documents in SharePoint 2013 `on premise`. Total document size was quite large {by 2023 standards}.
They wanted to migrate all documents to SharePoint Online {Microsoft 365}.

## 2. Custom Application for SharePoint 2013

I divided the _custom applications_ into 2 main groups:

- Farm solutions
    - .wsp files containing .dll files, WebPart, Application Page
- Non farm solution
    - UI using _Master Pages_
    - _Script Editor Web Part_

None of the applications had:

- Custom Field
- Custom Content Type
- Custom Event Receiver

## 3. UI for SharePoint Online

Challenge:

- Microsoft provided no sample or guideline on how to customize the UI for SharePoint Online.<br/>
- SharePoint Online has no concept of _Master Page_

Solution:<br/>

- explained in the article [UI for SharePoint Online with SPFx Extension](/en/UI-for-SharePoint-Online-with-SPFx-Extension)
- as a result, the SharePoint Online UI could be fully customized to match the client's requirements.

## 4. Custom Application - non SharePoint

Challenge:

- **A lot** of _custom applications_ {non SharePoint}
- Several vendors owned those _custom applications_:
    - I needed to coordinate with them
    - regarding application details and patching schedule

Action:

- one by one, each application was patched at the authentication layer
- PHP-based applications
- ASP.NET Web Form applications
- AngularJS FrontEnd applications

Technically, each application was patched as follows:

1. patch Authentication on the FrontEnd side only
2. patch Authentication on the BackEnd side
