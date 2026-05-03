---
ref: garis-webpage
judul: How to display a red outline on a WebPage
title: 'How to display a red outline on a WebPage'
description: 'A quick tip for displaying a red outline on all elements of a WebPage — useful for debugging and getting a big-picture view of the layout.'
tags: [general]
category: General
category_url: general
---

# How to display a red outline on a WebPage

As a _FrontEnd Developer_, I often need to see the "blocks" on a WebPage. A simple _red outline_ on all boxes is very helpful for:

- getting the _Big Picture_ of the WebPage layout
- Debugging

There are a few ways to do this:

- using plain `JavaScript`
- using `CSS`

## Using plain `JavaScript`

Run this script in the browser _console_:

```
document.querySelectorAll('*').forEach(el => {
    el.style.outline = '1px solid red';
});
```

## Using `CSS`

```
* {
  outline: 1px solid red !important;
}
```

or:

```
* {
  border: 1px solid red !important;
}
```

Result:

![Garis pada WebPage](/Aa_images/web-softwaredeveloperx-com/Outline-solid-red.png)
