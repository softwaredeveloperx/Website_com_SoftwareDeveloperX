---
ref: FrontEnd__Challenges_and_Strategy
judul: 'FrontEnd: Challenges and Strategy'
title: 'FrontEnd: Challenges and Strategy'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# FrontEnd: Challenges and Strategy

Situation:

I have a fairly complex system {[link](/en/Data_Model_part_1__Entity_DTO_Data_Transfer_Object/)}

- more than 500 tables
- FrontEnd has its own set of Challenges

At a high level, there are 2 Teams:

- Team A
    - Design - Business Process
        - Documentation files
    - Design - UI, using:
        - [figma.com](https://www.figma.com/)
        - [moqups.com](https://moqups.com/)
- Team X
    - Developer

> note: I wrote this article with the spirit of [Writing for 'Future of Me'](/en/Writing-for-Future-of-Me/)

## Strategy

To create a smooth working rhythm, I need a set of guidelines:

- define several _Big Tasks_, each with a specific goal
- CI / CD {Continuous Improvement / Continuous Development}

### FrontEnd

- HTML
    - _convert_ Design - UI to HTML
    - can be done using the tools above
    - or [Request: to AI effectively and efficiently {the right Tone}](/en/Request_to_AI_effectively_and_efficiently__the_right_Tone/)
- JavaScript
    - the part that _handles_ HTML
    - the part that _connects_ to the _end-point_ on the `BackEnd`

### BackEnd

- Part 1: Read Data
    - simple data {example: data for _Dropdown_}
    - data in _Tabular_
    - using guideline as written in article [Data Model part 2 - DTO {Data Transfer Object}](/en/Data_Model_part_2__DTO_Data_Transfer_Object/)
- Part 2: CRUD
    - Simple data
    - _Header - Detail_ data
    - data with columns in `JSON format`
- Part 3:
    - the _BackEnd_ part that implements the _Design - Business Process_

> notes for BackEnd:
>
> - building each Part separately helps avoid getting "stuck" on the BackEnd as a whole
> - start from the easiest part first:
>     - often what's _urgent_ is only the _BackEnd_ for "Read Data"
>     - while the more complex _BackEnd_ part {implementing _Design - Business Process_} can be built next

## GOAL: for the User / Client

At the end of the day, all this **technical** work is built for one purpose:

> a Product that actually works — for User/Client who use it.

That's the GOAL.<br/>
When in doubt about a decision, come back to that GOAL.<br/>

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
