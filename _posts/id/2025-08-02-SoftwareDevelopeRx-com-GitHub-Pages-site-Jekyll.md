---
ref: GitHub-Pages-site-Jekyll
judul: SoftwareDevelopeRx.com - GitHub Pages site - Jekyll
title: 'Membuat Website dengan GitHub Pages dan Jekyll - Setup softwaredeveloperx.com'
description: 'Cara setup website menggunakan GitHub Pages, Jekyll dengan theme minima, custom domain, dan konfigurasi jekyll-seo-tag.'
tags: [umum]
category: Umum
category_url: umum
---

# SoftwareDevelopeRx.com - GitHub Pages site - Jekyll

Tulisan berikut sebagai catatan untuk saya pribadi, seperti pada artikel [Menulis untuk 'Future of Me'](/id/Menulis-untuk-Future-of-Me/)

- Domain
- konfigurasi ke _GitHub Pages site_
- Jekyll sebagai _static site generator_
- setting theme: _minima_
    - file \_config.yml
    - folder: \_layout
    - folder: \_includes
- stategi:
    - Landing Page
        - untuk Homepage
        - per Topic / Category
    - Bilingual EN/ID

Website [softwaredeveloperx.com](https://softwaredeveloperx.com/) dihandle dengan cara:

- Github Pages ke Repo [https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io](https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io)
- menggunakan Jekyll {bisa diakses di [https://github.com/jekyll/jekyll](https://github.com/jekyll/jekyll)) atau di [https://jekyllrb.com](https://jekyllrb.com)}
- entry point: file `_config.yml`
- theme: `minima`

## Nice to have

- konfigurasi Github Pages ke Custom domain - softwaredeveloperx.com<br/>
  untuk Repo [https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io](https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io)
- file `CNAME`
- konfigurasi `Jekyll`

## Next step

- download theme `minima` di [https://github.com/jekyll/minima](https://github.com/jekyll/minima)
- extract pada _Root Folder_
- lakukan konfigurasi pada file [\_config.yml](https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io/blob/main/_config.yml)

### hasil extract theme: `minima`

![Jekyll--theme--minima](/Aa_images/web-softwaredeveloperx-com/Jekyll--theme--minima.png)

### konfigurasi Github Pages ke Custom domain - softwaredeveloperx.com

![Jekyll--theme--minima](/Aa_images/web-softwaredeveloperx-com/GitHub-Pages-Custom-domain.png)

### Deploy

proses Deploy bisa dilihat pada page berikut:

![GitHub-Pages-deploy.png](/Aa_images/web-softwaredeveloperx-com/GitHub-Pages-deploy.png)

## Summary: file added and changes

File-file yang saya tambahkan dan/atau ubah:

- file [\_config.yml](https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io/blob/main/_config.yml)
- file [index.md](https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io/blob/main/index.md)
- dan beberapa file pada beberapa Sub-Folder:

![GitHub-Pages-file-add-changes.png](/Aa_images/web-softwaredeveloperx-com/GitHub-Pages-file-add-changes.png)

## DO NOT: prefix \_

Underscore _ di Jekyll = tanda "ini folder/file sistem Jekyll, bukan konten publik".<br/>
Semua folder internal Jekyll pakai _:

```
_posts/      ← sistem
_layouts/    ← sistem
_includes/   ← sistem
_sass/       ← sistem
_drafts/     ← sistem
```

> ⚠️ _Warning:_
>
> saya pernah membuat file layout `_new_post.html` {fileName dengan prefix \_}, tetapi tidak bisa {karena alasan di atas}

## Google Search

Saya sama sekali tidak berniat, untuk bisa tampil di Google Search.<br/>
Dalam konteks Website, semua orang berhasil tampil di Google Search.<br>
Kenapa saya tidak bisa ?<br/>

Skill issue ?

Let's do that:

- plugin `jekyll-sitemap` ke file [\_config.yml](https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io/blob/main/_config.yml) <br/>
  sehingga akan terbentuk [https://softwaredeveloperx.com/sitemap.xml](https://softwaredeveloperx.com/sitemap.xml)
- daftar ke _Google Search Console_

![GitHub-Pages-file-add-changes.png](/Aa_images/web-softwaredeveloperx-com/google-search-console.png)

![GitHub-Pages-file-add-changes.png](/Aa_images/web-softwaredeveloperx-com/google-search-console-2.png)

## Landing Page dan Bilingual EN/ID

Saya mempunyai ide seperti berikut:

- Landing Page
    - untuk Homepage
    - per Topic / Category
- Bilingual EN/ID

Kombinasi akan menghasilkan:

- EN [https://softwaredeveloperx.com/](https://softwaredeveloperx.com/)
- ID [https://softwaredeveloperx.com/id/](https://softwaredeveloperx.com/id/)
- Topik SharePoint EN [https://softwaredeveloperx.com/sharepoint/](https://softwaredeveloperx.com/sharepoint/)
- Topik SharePoint ID [https://softwaredeveloperx.com/sharepoint-id/](https://softwaredeveloperx.com/sharepoint-id/)

How ?

![Landing-page-bilingual--EN-ID](/Aa_images/web-softwaredeveloperx-com/Landing-page-bilingual--EN-ID.png)

perhatikan gambar di atas:

- dimulai dari file [\_config.yml](https://github.com/softwaredeveloperx9/softwaredeveloperx9.github.io/blob/main/_config.yml)
- selanjutnya folder: `_layout` dan `_includes`
- dan beberapa file:
    - index.md
    - id.md
    - sharepoint.md
    - sharepoint-id.md
    - tulisan.md
    - contents.md
    - ... {dan file-file .md lainnya}

## Why Bilingual EN/ID ? bukankah sudah ada AI ?

Saya cukup fasih dalam berbicara dan menulis dalam Bahasa Indonesia.<br/>
My English ?<br/>
not too good<br/>

Saya berharap, saya mulai belajar untuk _writing in English_.<br/>
Even though in the very beginning, I request AI helping me.
