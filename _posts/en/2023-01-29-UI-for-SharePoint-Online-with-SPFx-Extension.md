---
ref: UI-for-SharePoint-Online-with-SPFx-Extension
judul: UI for SharePoint Online with SPFx Extension
title: 'Custom UI for SharePoint Online using SPFx Extension'
description: 'How to build a custom UI for SharePoint Online using SPFx Extension to override CSS, handle the flicker problem, and allow easy style changes without redeployment.'
tags: [sharepoint]
category: SharePoint
category_url: 'sharepoint'
---

# UI for SharePoint Online

**Challenge:**

- Microsoft provides no detailed guideline or sample on how to customize the UI for SharePoint Online.<br/>
    - only a simple _color picker_ for the SharePoint Online `Theme`
- SharePoint Online has no concept of `Master Page` {unlike SharePoint 2013}

**Solution:**

- build a _custom_ `Extension` using _SPFx: SharePoint Framework_
- the Extension loads a .css style file

I created 2 groups of .css styles:

1. embedded inside the Extension itself
2. a .css file placed in a Document Library folder

**Why?**

- why not just one place?
- why does it need to be in 2 places?

**Because:**

1. Timing + Flicker
2. Easy to modify

**Situation**

> SharePoint Online loads many .css files of its own

**The chosen approach**

> We need to _override_ some of SharePoint Online's built-in styles.

**How it works:**

- our .css styles must be loaded at the right _Timing_
- if not, a _Flicker_ will occur:
    - SharePoint Online first renders its own Theme {which we can partially configure}
    - usually a Blue color
    - then our .css kicks in
    - the user sees a visible _Flicker_ on the screen
- Easy to modify:
    - we often need CSS changes — without going through the full Develop/Deploy cycle for _custom SPFx_

**Summary**

> With all these techniques combined, we can easily achieve a UI that fully matches the user's requirements, fully integrated with SharePoint Online
