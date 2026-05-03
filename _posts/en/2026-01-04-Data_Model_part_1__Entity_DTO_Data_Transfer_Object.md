---
ref: Data_Model_part_1__Entity_DTO_Data_Transfer_Object
judul: 'Data Model part 1 - Entity, DTO {Data Transfer Object}'
title: 'Data Model part 1 - Entity, DTO {Data Transfer Object}'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# Data Model part 1 - Entity, DTO {Data Transfer Object}

Situation:

I have a fairly complex system

- a large number of Tables {more than 500 tables}
- a large number of Columns {1 Table can have more than 50 columns}
- Security {data sensitivity}

<table border="1" cellpadding="6" cellspacing="0" style="width:500px">
  <thead>
    <tr>
      <th>Object</th>
      <th>Columns</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="2"><strong>Sales Order</strong></td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Header</td>
      <td>more than 80</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Items</td>
      <td>more than 50</td>
    </tr>
    <tr>
      <td colspan="2"><strong>Shipment Request</strong></td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Header</td>
      <td>more than 50</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Items</td>
      <td>more than 50</td>
    </tr>
    <tr>
      <td colspan="2"><strong>Delivery Order</strong></td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Header</td>
      <td>more than 80</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Items</td>
      <td>more than 50</td>
    </tr>
    <tr>
      <td colspan="2"><strong>Purchase Order</strong></td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Header</td>
      <td>more than 50</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Items</td>
      <td>more than 50</td>
    </tr>
  </tbody>
</table>

Objective:
<br/>I need a `Guideline` for the _Data Model_, that is:

- aligned with the Business Process
    - specific to my own Business Process
    - may differ from / be unconventional for other Systems {_no problem_}
- simple
    - relatively easy to implement
- consistent
    - consistent across each Object
    - consistent in terms of `naming convention`

What-if: I don't have that `Guideline`?

- A fairly complex system like the one above → difficult to Develop
- also difficult to Maintain
- changes and/or additions to columns/fields can cause related parts to be forgotten and left out of sync

> Note:
> <br/>even with a `Guideline` in place, there is still a _Challenge_ around the topic of `out of sync`

**DTO: Data Transfer Object** — _a quick concept overview_

- in a complex system, not all data from the Database needs to be sent to the FrontEnd
- `Entity` → a direct representation of a `Table` in the Database
- `DTO` → the "shape" of data sent between Layers {BackEnd to FrontEnd, or between Services}

> `Entity` ≠ `DTO`<br/>
> Entity is for the Database. DTO is for communication between Layers.

<img src="/Aa_images/web-softwaredeveloperx-com/Diagrams/Data-Model.svg" />

**Database Object**

- Table
    - actual data
- View
    - View directly to a Table
    - View to another View

**DTO: Data Transfer Object**<br/>
discussed in more detail in the article _Data Model part 2 - DTO {Data Transfer Object}_ [link](/en/Data_Model_part_2__DTO_Data_Transfer_Object/)

_Challenge_ around the topic of `out of sync`<br/>
discussed in the articles:

- _Data Model part 3 - out of sync Database Object {Table, View} vs Model {BackEnd}_ [link](/en/Data_Model_part_3__out_of_sync_DB_Object_vs__Model_BackEnd/)
- _Data Model part 4 - out of sync Model {BackEnd} vs Types {FrontEnd}_ [link](/en/Data_Model_part_4__out_of_sync_Model_BackEnd_vs_Types_FrontEnd/)

> This Guideline is not about perfectionism —  
> it is about consistency.
>
> - consistent in naming
> - consistent in structure
>   <br/>so that a complex system remains navigable.

**Implementation Example:**

- Table: Sales Order
    - Header with more than 80 columns
    - Items with more than 50 columns
- Not everything will be used on the FrontEnd {HTML View} with a _one to one_ mapping
- there are mechanisms for:
    - column restriction
    - Masking
