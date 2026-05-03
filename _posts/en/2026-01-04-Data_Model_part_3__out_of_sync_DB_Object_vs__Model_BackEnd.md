---
ref: Data_Model_part_3__out_of_sync_DB_Object_vs__Model_BackEnd
judul: 'Data Model part 3 - out of sync Database Object {Table, View} vs Model {BackEnd}'
title: 'Data Model part 3 - out of sync Database Object {Table, View} vs Model {BackEnd}'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# Data Model part 3 - out of sync Database Object {Table, View} vs Model {BackEnd}

## Situation

**out of sync Database Object {Table, View} vs Model {BackEnd}** can happen due to:

- Add / Update / Delete processes
- on the Database Object {Table, View}
- as well as on the Model {BackEnd}

<img src="/Aa_images/web-softwaredeveloperx-com/Diagrams/Data-Model--out_of_sync_DB_Object_vs__Model_BackEnd.svg" />

## Solution

Use a `Prompt` like the following:

I have A: {fileName_DB_Object.sql}<br/>
I have B: {fileName.cs}

please check B, fix anything that is "not correct":

- based on A

> This `Prompt` pattern is an implementation of:  
> [Request: to AI effectively and efficiently](/en/Request_to_AI_effectively_and_efficiently__the_right_Tone/)

`Guideline`:

- Database Object {Table, View}
- as the "Source"

**Example case: a new column in the Database, forgotten to be updated in the Model {BackEnd}**

Situation:

- a new column: `ApprovalStatus` was added to the Sales Order `Table`
- the Model {BackEnd} was **not updated**

The effect:

- when Writing data → the `ApprovalStatus` column is always `NULL` in the Database
- when Reading data → the `ApprovalStatus` field is absent from the API response
- FrontEnd cannot display data that should be there
- bugs like this are **hard to trace** — no error is thrown, data just "silently disappears"

> _silent bug_ — more dangerous than an obvious error

**Why is the Database Object the "Source of Truth"?**

- The Database is the final _endpoint_ of the data
- if the Database and Model are out of sync → stored data can be wrong, or data cannot be read
- conversely: if the Model is used as the "Source" → risk of _mismatch_ with the actual Database structure

> Database Object = ground truth<br/>
> Model BackEnd = must follow the Database
