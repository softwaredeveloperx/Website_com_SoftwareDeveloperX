---
ref: Example_MD_File__Document_Driven_Development
judul: 'Example .MD File, for Document Driven Development'
title: 'Example .MD File, for Document Driven Development'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# Example .MD File, for Document Driven Development

I create a .MD File, with "Marking" as follows:

- section for linking to an Image
    - this image can serve as a "Visualization"
    - it can also be useful for "sync" with the HTML View, i.e. `file_something.html`
- Implementation - Related files:
    - this section, besides providing Implementation-related information
    - is also useful for "sync"
- Mapping
    - there are 2, namely:
        - Mapping: Data Format - View
        - Mapping: Items
    - can be used as a reference for the HTML View, i.e. `file_something.html`
    - can also be used for `E2E {end-to-end} Testing Script`

````md
> **Note:** this is a brief description

![just a caption](../A_images/path_to_image_File.png)

# Description:

{this is the Description section}

# UI:

- Toolbar
- Form

# Implementation - Related files:

- `file_something.html`
- `file_something.js`
- `file_something.cs`

## Data Format:

```json
{}
```

## Mapping: Data Format - View

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
