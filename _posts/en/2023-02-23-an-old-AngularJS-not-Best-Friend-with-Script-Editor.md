---
ref: an-old-AngularJS-bukan-Best-Friend-dengan-Script-Editor
judul: an old AngularJS is not Best Friend with Script Editor
title: 'an old AngularJS is not Best Friend with Script Editor'
description: 'Why old AngularJS applications cannot be reliably loaded using Script Editor in SharePoint Online, and how the problem was solved.'
tags: [sharepoint]
category: SharePoint
category_url: 'sharepoint'
---

# an old AngularJS is not Best Friend with Script Editor

In the context of my project [Migration SharePoint 2013 to SharePoint Online](/en/Migration-SharePoint-2013-to-SharePoint-Online/),<br/>
the client had quite a number of AngularJS applications running on top of SharePoint 2013.

## Situation:

- AngularJS == ok with `Script Editor` in SharePoint 2013
- AngularJS with `Script Editor` in SharePoint Online:
    - works fine for simple scripts
    - breaks down once there are many Services involved

I was convinced it was a `Timing` issue, as I explained in [Script Editor for SharePoint Online, Challenges and Solutions](/en/Script-Editor-for-SharePoint-Online/), but I simply could not get it to run smoothly.

## Solution:

- Convert the AngularJS applications to JQuery
- or another Framework

## At the End:

- I converted several AngularJS-based applications to JQuery
- all running ok
