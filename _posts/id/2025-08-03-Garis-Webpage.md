---
ref: garis-webpage
judul: Cara menampilkan Garis merah pada WebPage
title: 'Cara menampilkan Garis merah pada WebPage'
description: 'Cara menampilkan Garis merah pada WebPage'
tags: [umum]
category: Umum
category_url: umum
---

# Cara menampilkan Garis merah pada WebPage

Sebagai _FrontEnd Developer_, saya sering memerlukan informasi "block-block" pada suatu WebPage. Simple _garis merah_ di semua Kotak, akan sangat membantu:

- memberikan _Big Picture_ WebPage
- melakukan Debugging

Ada beberapa cara:

- menggunakan simple - `JavaScript`
- menggunakan `CSS`

## Menggunakan simple - `JavaScript`

Gunakan script berikut pada _console_:

```
document.querySelectorAll('*').forEach(el => {
    el.style.outline = '1px solid red';
});

```

## Menggunakan `CSS`

```
* {
  outline: 1px solid red !important;
}

```

atau:

```

* {
  border: 1px solid red !important;
}

```

hasil seperti berikut:

![Garis pada WebPage](/Aa_images/web-softwaredeveloperx-com/Outline-solid-red.png)
