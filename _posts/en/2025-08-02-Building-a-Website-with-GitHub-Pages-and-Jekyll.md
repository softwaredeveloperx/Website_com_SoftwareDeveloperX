---
ref: GitHub-Pages-site-Jekyll
judul: SoftwareDevelopeRx.com - GitHub Pages site - Jekyll
title: 'Building a Website with GitHub Pages and Jekyll - Setup softwaredeveloperx.com'
description: 'How to set up a website using GitHub Pages, Jekyll with the minima theme, custom domain, and jekyll-seo-tag configuration.'
tags: [general]
category: General
category_url: general
---

# SoftwareDevelopeRx.com - GitHub Pages site - Jekyll

The following is a personal note, as mentioned in the article [Writing for 'Future of Me'](/en/Writing-for-Future-of-Me/)

- Domain
- configuration to _GitHub Pages site_
- Jekyll as a _static site generator_
- setting the theme: _minima_
    - file \_config.yml
    - folder: \_layout
    - folder: \_includes
- strategy:
    - Landing Page
        - for Homepage
        - per Topic / Category
    - Bilingual EN/ID

The website [softwaredeveloperx.com](https://softwaredeveloperx.com/) is handled as follows:

- GitHub Pages connected to the Repo [https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io](https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io)
- using Jekyll {available at [https://github.com/jekyll/jekyll](https://github.com/jekyll/jekyll) or [https://jekyllrb.com](https://jekyllrb.com)}
- entry point: `_config.yml` file
- theme: `minima`

## Nice to have

- configure GitHub Pages to use Custom domain - softwaredeveloperx.com<br/>
  for Repo [https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io](https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io)
- `CNAME` file
- `Jekyll` configuration

## Next step

- download the `minima` theme at [https://github.com/jekyll/minima](https://github.com/jekyll/minima)
- extract to the _Root Folder_
- configure the [\_config.yml](https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io/blob/main/_config.yml) file

### Result after extracting the `minima` theme

![Jekyll--theme--minima](/Aa_images/web-softwaredeveloperx-com/Jekyll--theme--minima.png)

### Configuring GitHub Pages with Custom domain - softwaredeveloperx.com

![Jekyll--theme--minima](/Aa_images/web-softwaredeveloperx-com/GitHub-Pages-Custom-domain.png)

### Deploy

The deployment process can be seen here:

![GitHub-Pages-deploy.png](/Aa_images/web-softwaredeveloperx-com/GitHub-Pages-deploy.png)

## Summary: files added and changed

Files I added and/or modified:

- [\_config.yml](https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io/blob/main/_config.yml)
- [index.md](https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io/blob/main/index.md)
- and several files across multiple Sub-Folders:

![GitHub-Pages-file-add-changes.png](/Aa_images/web-softwaredeveloperx-com/GitHub-Pages-file-add-changes.png)

## DO NOT: prefix \_

Underscore _ in Jekyll = "this is a Jekyll system folder/file, not public content".<br/>
All Jekyll internal folders use _:

```
_posts/      ← system
_layouts/    ← system
_includes/   ← system
_sass/       ← system
_drafts/     ← system
```

> ⚠️ _Warning:_
>
> I once created a layout file called `_new_post.html` {fileName with \_ prefix}, but it did not work {for the reason above}

## Google Search

I had no intention at all of appearing in Google Search.<br/>
But in the context of a website, everyone manages to show up in Google Search.<br/>
Why couldn't I?<br/>

Skill issue?

Let's do that:

- add plugin `jekyll-sitemap` to [\_config.yml](https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io/blob/main/_config.yml)<br/>
  so that [https://softwaredeveloperx.com/sitemap.xml](https://softwaredeveloperx.com/sitemap.xml) is generated
- register to _Google Search Console_

![GitHub-Pages-file-add-changes.png](/Aa_images/web-softwaredeveloperx-com/google-search-console.png)

![GitHub-Pages-file-add-changes.png](/Aa_images/web-softwaredeveloperx-com/google-search-console-2.png)

## Landing Page and Bilingual EN/ID

My idea was as follows:

- Landing Page
    - for Homepage
    - per Topic / Category
- Bilingual EN/ID

The combination produces:

- EN [https://softwaredeveloperx.com/](https://softwaredeveloperx.com/)
- ID [https://softwaredeveloperx.com/id/](https://softwaredeveloperx.com/id/)
- SharePoint topic EN [https://softwaredeveloperx.com/sharepoint/](https://softwaredeveloperx.com/sharepoint/)
- SharePoint topic ID [https://softwaredeveloperx.com/sharepoint-id/](https://softwaredeveloperx.com/sharepoint-id/)

How?

![Landing-page-bilingual--EN-ID](/Aa_images/web-softwaredeveloperx-com/Landing-page-bilingual--EN-ID.png)

Looking at the image above:

- it starts from [\_config.yml](https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io/blob/main/_config.yml)
- then the folders: `_layout` and `_includes`
- and several files:
    - index.md
    - id.md
    - sharepoint.md
    - sharepoint-id.md
    - tulisan.md
    - contents.md
    - ... {and other .md files}

## Why Bilingual EN/ID? Isn't AI enough?

I am fairly fluent in speaking and writing in Bahasa Indonesia.<br/>
My English?<br/>
not too good<br/>

I hope to start learning to _write in English_.<br/>
Even though in the very beginning, I requested AI to help me.
