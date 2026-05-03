---
ref: Refine_Document__Review_Revise
judul: "Refine Document: Review and Revise"
title: "Refine Document: Review and Revise"
description: ''
tags: [ide]
category: Ide
category_url: ide
---

# Refine Document: Review and Revise

## Situasi
- saya mempunyai {.MD file} sebagai _Specification Document_ (acuan untuk _Development_)
- saya perlu melakukan Refine (Review and Revise) terhadap {.MD file} ini
- {.MD file} berupa:
  - text file
  - bisa juga berisi link ke beberapa image

## Request

Tolong proses `Refine` (Review and Revise) terhadap {.MD file} tersebut (juga terhadap beberapa image - jika ada).

- Fokus A: Correctness
  - Clear
  - Unambiguous
  - Precise
- Fokus B: Error Detection 🎯
  - Error Logic
  - Missing section
  - Incomplete
- Fokus C: Improvement 🚀
  - Suggestion
  - Optimization
  - Alternative _(opsional — tambahkan hanya jika relevan)_
  
## Expected Result
- dalam bentuk 2 .MD file
- Review
  - tulis dalam bentuk .MD file yang baru
- Revise:
  - update {.MD file} input
  - hanya insert terhadap Esensi perubahan
    - Definisi: perubahan yang memperbaiki error logic, menghilangkan ambiguitas, atau mengisi bagian yang hilang — bukan perubahan kosmetik/formatting
  - tolong jangan dilakukan Formatting file
  - jika kamu fikir, perlu dilakukan perubahan urutan suatu bagian, maka tolong buat menjadi .MD file yang baru (sehingga Result menjadi 3 .MD file)

## Catatan

Too Few vs Too Much

```
❌ Too Few   → Incomplete, tidak berguna
❌ Too Much  → Overwhelmed, kebanjiran informasi
✅ Pragmatic
```

Kamu harus menemukan _sweet spot_ -- yang "pas".
