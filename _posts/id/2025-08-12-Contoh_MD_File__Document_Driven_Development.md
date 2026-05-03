---
ref: Contoh_MD_File__Document_Driven_Development
judul: 'Contoh .MD File, untuk Document Driven Development'
title: 'Contoh .MD File, untuk Document Driven Development'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# Contoh .MD File, untuk Document Driven Development

Saya membuat suatu .MD File, dengan "Marking" sebagai berikut:

- bagian untuk link ke Image
    - image ini, bisa berguna sebagai "Visualisasi"
    - bisa juga berguna untuk "sync" ke View HTML, yaitu `file_something.html`
- Implementasi - Related files:
    - bagian ini selain sebagai informasi terkait Implementasi
    - juga berguna untuk "sync"
- Mapping
    - ada 2, yaitu
        - Mapping: Format data - View
        - Mapping: Items
    - bisa digunakan sebagai acuan ke View HTML, yaitu `file_something.html`
    - juga bisa digunakan untuk `E2E {end-to-end} Testing Script`

````md
> **Note:** ini keterangan singkat

![hanya keterangan saja](../A_images/path_to_image_File.png)

# Deskripsi:

{ini bagian Deskripsi}

# UI:

- Toolbar
- Form

# Implementasi - Related files:

- `file_something.html`
- `file_something.js`
- `file_something.cs`

## Format data:

```json
{}
```

## Mapping: Format data - View

| Label - Form | Field       | Type                | Mandatory |
| ------------ | ----------- | ------------------- | --------- |
| Branch       | Branch      | Dropdown to Service | Yes       |
| Warehouse    | Warehouse   | Dropdown to Service | Yes       |
| Notes        | Description | Textarea            |           |

## Mapping: Items

| Label - Form | Field       | Type          | Mandatory | Notes     |
| ------------ | ----------- | ------------- | --------- | --------- |
| Item Code    | ItemCode    | Typeahead_row | Yes       |           |
| Description  | Description | Text          |           | Read_only |
| Qty 1        | Qty1        | Number        |           |           |
| Comments     | Comments    |               |           |           |
````
