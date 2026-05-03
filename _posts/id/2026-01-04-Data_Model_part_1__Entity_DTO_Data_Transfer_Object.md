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

Situasi:

saya mempunyai system yang cukup kompleks

- banyak sekali Table {lebih dari 500 table}
- banyak sekali Columns {1 Table bisa mempunyai lebih dari 50 column}
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
      <td>lebih dari 80</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Items</td>
      <td>lebih dari 50</td>
    </tr>
    <tr>
      <td colspan="2"><strong>Shipment Request</strong></td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Header</td>
      <td>lebih dari 50</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Items</td>
      <td>lebih dari 50</td>
    </tr>
    <tr>
      <td colspan="2"><strong>Delivery Order</strong></td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Header</td>
      <td>lebih dari 80</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Items</td>
      <td>lebih dari 50</td>
    </tr>
    <tr>
      <td colspan="2"><strong>Purchase Order</strong></td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Header</td>
      <td>lebih dari 50</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;Items</td>
      <td>lebih dari 50</td>
    </tr>
  </tbody>
</table>

Objective:
<br/>Saya memerlukan `Guideline` untuk _Data Model_, yang:

- sesuai dengan Business Process
    - spesifik untuk Business Process milik saya
    - mungkin berbeda / tidak lazim bagi System lain {_no problem_}
- simple
    - relatif mudah diimplementasikan
- konsisten
    - konsisten pada masing-masing Object
    - konsisten terkait `naming convention`

What-if: saya tidak punya `Guideline` tersebut ?

- System yang cukup kompleks seperti di atas --> susah untuk di Develop
- susah juga untuk di Maintain
- perubahan and/or penambahan column/field, bisa membuat lupa untuk update bagian yang related

> Note:
> <br/>dengan mempunyai `Guideline` saja, masih ada _Challenge_ dengan topik `out of sync`

**DTO: Data Transfer Object** — _sekilas konsep_

- pada sistem yang kompleks, tidak semua data dari Database perlu dikirim ke FrontEnd
- `Entity` → representasi langsung dari `Table` di Database
- `DTO` → "bentuk" data yang dikirim antar Layer {BackEnd ke FrontEnd, atau antar Service}

> `Entity` ≠ `DTO`<br/>
> Entity untuk Database. DTO untuk komunikasi antar Layer.

<img src="/Aa_images/web-softwaredeveloperx-com/Diagrams/Data-Model.svg" />

**Database Object**

- Table
    - actual data
- View
    - View langsung ke Table
    - View ke View lainnya

**DTO: Data Transfer Object**<br/>
dibahas lebih detail pada artikel _Data Model part 2 - DTO {Data Transfer Object}_ [link](/id/Data_Model_part_2__DTO_Data_Transfer_Object/)

_Challenge_ dengan topik `out of sync`<br/>
dibahas pada artikel:

- _Data Model part 3 - out of sync Database Object {Table, View} vs Model {BackEnd}_ [link](/id/Data_Model_part_3__out_of_sync_DB_Object_vs__Model_BackEnd/)
- _Data Model part 4 - out of sync Model {BackEnd} vs Types {FrontEnd}_ [link](/id/Data_Model_part_4__out_of_sync_Model_BackEnd_vs_Types_FrontEnd/)

> Guideline ini bukan tentang perfectionism —  
> melainkan tentang consistency.
>
> - konsisten dalam naming
> - konsisten dalam structure
>   <br/>sehingga sistem yang kompleks tetap bisa di-navigate.

**Contoh Implementasi:**

- Table: Sales Order
    - Header dengan lebih dari 80 columns
    - Items dengan lebih dari 50 columns
- Tidak lantas semuanya akan digunakan pada FrontEnd {bagian View HTML} dengan mapping _one to one_
- ada mekanisme:
    - dengan pembatasan column
    - dengan Masking
