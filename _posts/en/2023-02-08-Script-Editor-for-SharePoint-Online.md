---
ref: Script-Editor-for-SharePoint-Online
judul: Script Editor for SharePoint Online, Challenges and Solutions
title: 'Script Editor for SharePoint Online, Challenges and Solutions'
description: 'How to display script/html/css in SharePoint Online, along with the challenges encountered and practical solutions.'
tags: [sharepoint]
category: SharePoint
category_url: 'sharepoint'
---

# Script Editor for SharePoint Online, Challenges and Solutions

I often take a pragmatic approach ([the Pragmatic Programmer](https://en.wikipedia.org/wiki/The_Pragmatic_Programmer)), focused on:

1. Solve the problem
2. Not Perfectionist
    - avoid `Over Engineering`
    - Good > Perfect
    - Shipment {Delivery} the Result {writing, `Code`, ...}

This same mindset carries over to custom application development on SharePoint Online.<br/>
SPFx is very good, but for a simple script? No thanks.

- setting up SPFx
- React and all its dependencies
- all of it totals around 600 MB

## My journey:

- SharePoint 2010/2013
    - Server Side: [WebPart to load .ascx file in SharePoint WSS 3 / MOSS 2007](/en/WebPart-to-load-ascx-file-in-SharePoint-WSS-3-MOSS-2007/)
    - Client Side: Script Editor {standard SharePoint WebPart}
- SharePoint Online
    - Script editor web part for modern pages: [react-script-editor](https://github.com/pnp/sp-dev-fx-webparts/tree/main/samples/react-script-editor)<br/>

> I think the name `react-script-editor` is misleading.
> Users might think it loads `React Script`, but it is actually a WebPart for loading script/html/css
> that happens to be built using `React`

## My favourite approach for custom apps on SharePoint Online:

1. develop SPFx Extension for UI/Theme
2. JavaScript/HTML/CSS loaded by `react-script-editor`
3. if option 2 has issues {usually around `get Token` in SharePoint Online}<br/>
   then: develop SPFx WebPart

## Challenge

1. The usual suspect: `Timing` issues with JavaScript
    - especially common in applications that depend on other modules
    - understandable, if you look at the _Internal - how `react-script-editor` works_
2. Page Load
    - in SharePoint Online, navigating from one page to another often does not trigger a full page reload
        - perhaps that is by design in SharePoint Online
        - perhaps it is common across modern web apps in general
        - I am not entirely sure
    - the side effect: our application logic can break

## Solution

- be aware of the _Timing_ situation described above
- it can be handled by checking a Flag/Condition
