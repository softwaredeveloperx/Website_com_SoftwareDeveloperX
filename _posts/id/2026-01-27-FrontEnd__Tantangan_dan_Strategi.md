---
ref: FrontEnd__Tantangan_dan_Strategi
judul: 'FrontEnd: Tantangan dan Strategi'
title: 'FrontEnd: Tantangan dan Strategi'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# FrontEnd: Tantangan dan Strategi

Situasi:

saya mempunyai system yang cukup kompleks {[link](/id/Data_Model_part_1__Entity_DTO_Data_Transfer_Object/)}

- lebih dari 500 table
- FrontEnd mempunyai Tantangan tersendiri

Secara garis besar, ada 2 Team:

- Team A
    - Design - Business Process
        - file Dokumentasi
    - Design - UI, menggunakan:
        - [figma.com](https://www.figma.com/)
        - [moqups.com](https://moqups.com/)
- Team X
    - Developer

> catatan: saya menulis artikel ini, dengan semangat [Menulis untuk 'Future of Me'](/id/Menulis-untuk-Future-of-Me/)

## Strategi

Untuk membuat irama kerja yang smooth, saya memerlukan suatu pedoman:

- membuat beberapa _Task Besar_, dengan tujuan yang spesifik
- CI / CD {Continuous Improvement / Continuous Development}

### FrontEnd

- HTML
    - _convert_ Design - UI ke HTML
    - bisa dengan menggunakan Tools di atas
    - atau [Request: ke AI secara efektif dan efisien {Tone yang tepat}](/id/Request_ke_AI_secara_efektif_dan_efisien__Tone_yang_tepat/)
- JavaScript
    - bagian untuk _handle_ HTML
    - bagian untuk _connect_ ke _end-point_ di `BackEnd`

### BackEnd

- Part 1: Read Data
    - data Simple {contoh: data untuk _Dropdown_}
    - data berupa _Tabular_
    - menggunakan teknik sesuai artikel [Data Model part 2 - DTO {Data Transfer Object}](/id/Data_Model_part_2__DTO_Data_Transfer_Object/)
- Part 2: CRUD
    - data Simple
    - data _Header - Detail_
    - data dengan kolom berupa `JSON format`
- Part 3:
    - bagian _BackEnd_ yang merupakan implementasi _Design - Business Process_

> catatan untuk _BackEnd_:
>
> - masing-masing Part dibuat untuk menghindari "stuck" pada _BackEnd_ -- secara keseluruhan
> - bisa dimulai dari yang paling mudah:
>     - seringkali yang _urgent_ diperlukan: bagian _BackEnd_ untuk "Read Data" saja
>     - sedangkan bagian _BackEnd_ yang lebih kompleks {implementasi _Design - Business Process_}, bisa dibuat berikutnya

## GOAL: untuk User / Client

Pada akhirnya, semua hal **teknis** diatas untuk satu tujuan:

> sebuah Product yang benar-benar berfungsi — untuk User/Client yang menggunakannya.

Itulah GOAL-nya.<br/>
Ketika ragu dalam mengambil keputusan, kembali ke GOAL tersebut.<br/>

## Checklist

<table style="width:100%; border-collapse: collapse; font-size: 14px;">
  <thead>
    <tr style="border-bottom: 1px solid #ccc;">
      <th style="text-align: left; padding: 6px 10px;">Task</th>
      <th style="text-align: center; padding: 6px 10px; width: 50px;">Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td colspan="2" style="padding: 8px 10px 2px; font-weight: bold; color: #555; font-size: 13px;">A. Document</td>
    </tr>
    <tr style="border-bottom: 1px solid #eee;">
      <td style="padding: 4px 10px 4px 24px;">o Design — Business Process</td>
      <td></td>
    </tr>
    <tr style="border-bottom: 1px solid #eee;">
      <td style="padding: 4px 10px 4px 24px;">o Design — UI</td>
      <td></td>
    </tr>
    <tr>
      <td colspan="2" style="padding: 8px 10px 2px; font-weight: bold; color: #555; font-size: 13px;">B. Development</td>
    </tr>
    <tr>
      <td style="padding: 4px 10px 4px 24px; font-weight: bold;">o FrontEnd</td>
      <td></td>
    </tr>
    <tr>
      <td style="padding: 4px 10px 4px 40px;">x HTML</td>
      <td></td>
    </tr>
    <tr>
      <td style="padding: 4px 10px 4px 40px;">x JavaScript</td>
      <td></td>
    </tr>
    <tr>
      <td style="padding: 4px 10px 4px 56px; color: #666;">o handle HTML</td>
      <td></td>
    </tr>
    <tr style="border-bottom: 1px solid #eee;">
      <td style="padding: 4px 10px 4px 56px; color: #666;">o connect to end-point of BackEnd</td>
      <td></td>
    </tr>
    <tr>
      <td style="padding: 4px 10px 4px 24px; font-weight: bold;">o BackEnd</td>
      <td></td>
    </tr>
    <tr>
      <td style="padding: 4px 10px 4px 40px;">x part 1: Read Data</td>
      <td></td>
    </tr>
    <tr>
      <td style="padding: 4px 10px 4px 40px;">x part 2: CRUD</td>
      <td></td>
    </tr>
    <tr>
      <td style="padding: 4px 10px 4px 40px;">x part 3: implement the Design — Business Process</td>
      <td></td>
    </tr>
  </tbody>
</table>

## Reminder - SDR:

**S** {Situation → Specific → Simple → Speed → **Shipment**}<br/>
**D** {Define → Document → Design → Develop → **Delivery**}<br/>
**R** {Realistic → Refine → **Result**}
