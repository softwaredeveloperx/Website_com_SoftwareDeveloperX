---
ref: Document_Driven_Development__Specification_Document__Source_of_Truth
judul: 'Document Driven Development - Specification Document (Source of Truth)'
title: 'Document Driven Development - Specification Document (Source of Truth)'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# Document Driven Development - Specification Document (Source of Truth)

Situation:

I have a fairly complex system, which I explained in the article [Data Model part 1 - Entity, DTO {Data Transfer Object}](/en/Data_Model_part_1__Entity_DTO_Data_Transfer_Object/)

<img src="/Aa_images/web-softwaredeveloperx-com/Diagrams/Data-Model.svg" />

- data flows from one part to another
- data flows from one Layer to another
- example: the HTML View should never "link" to the wrong fieldName {Model}
- Next:
    - E2E Testing Script {nowadays, this _is a must_ (no longer just _nice to have_)}
    - ideally, Testing Scripts can be generated using a `Generator`

Objective:
<br/>I need a `Source of Truth` as a reference for all Components in the system

## .MD File as `Source of Truth` - Specification Document

I use .MD files, because:

- easy to read
- easy to apply some "Marking"
- simple _Text File_
- on GitHub, Copy/Paste images into a .MD file == very easy

As I wrote in the article [How to write a .MD file](/en/How-to-write-a-MD-file/), in the section:

Too Few vs Too Much

```
❌ Too Few   → Incomplete, not useful
❌ Too Much  → Overwhelmed, information overload
✅ Pragmatic
```

I need to find the _sweet spot_ — the one that feels "just right".

So I divide .MD files into at least a few categories:

- Type 1: .MD file as a `Specification Document`:
    - about the technical details of a Tool
    - about the Business Flow that must be implemented by Code
    - a combination of both
- Type 2: .MD file as input for a Tool
- Type 3: .MD file as a User Guide

This at least reduces _distraction_ for the reader.<br/>
For example:

- a [.MD file for `Specification Document`] doesn't need to explain how to use a tool
- that causes a loss of focus {I experience this often}

<img src="/Aa_images/web-softwaredeveloperx-com/Diagrams/Document_Driven_Development.png" />

As shown in the image above, everything references the .MD file {as the `Source of Truth` - Specification Document}

- keep in mind that it's not just 1 type of .MD file
- but there are at least 3 Types of .MD files, as explained above

## A `Generator` can be built, because the `Source of Truth` is already available

There will be at least a few Generators, namely:

```
generator__Test_script.mjs
generator__Test_script__items.mjs

generator__md_to_excel.mjs
generator__md_to_excel__items.mjs
```

I wrote about this in the article [E2E {end-to-end} Testing: 4 types of Testing Script](/en/E2E__end_to_end_Testing__4_tipe_Testing_Script/) in the section _Generator: automatically generating - Testing Scripts_

## WHAT NOT

- Generator - Form / UI

### WHY NOT ?

- rather than building a `Generator - Form / UI` {because Form/UI tends to be fairly complex}
- it is better to use a `Request to -- AI` to generate a Form / UI<br/>

example: article [Request to AI effectively and efficiently {the right Tone}](/en/Request_to_AI_effectively_and_efficiently__the_right_Tone/) in the section `Case study 1: Request - generate Code from an Image`

## Example .MD File, for Document Driven Development

I discuss Example .MD Files [here](/en/Example_MD_File__Document_Driven_Development/)
