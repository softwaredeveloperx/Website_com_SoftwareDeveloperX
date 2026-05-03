---
ref: Request_ke_AI_secara_efektif_dan_efisien__Tone_yang_tepat
judul: 'Request: ke AI secara efektif dan efisien {Tone yang tepat}'
title: 'Request: ke AI secara efektif dan efisien {Tone yang tepat}'
description: ''
tags: [renungan]
category: Renungan
category_url: renungan
---

# Request: ke AI secara efektif dan efisien {Tone yang tepat}

## Situasi:

saya memerlukan cara yang efektif dan efisien, untuk request sesuatu ke AI:

- tidak ada over-explaining
- tidak ada paragraf panjang
- AI langsung paham **semua yang dibutuhkan**

## Solusi

- berikan **konteks yang cukup**
- bukan _instruksi yang berlebihan_

Too Few vs Too Much

```
❌ Too Few   → Incomplete, tidak berguna
❌ Too Much  → Overwhelmed, kebanjiran informasi
✅ Pragmatic
```

saya harus menemukan _sweet spot_ -- yang "pas".

## Tone yang tepat

bukan instruksi yang kaku seperti:
"buatkan saya kode untuk..."

melainkan seperti berbicara ke _teammate_ yang **sangat cerdas**:<br/>

> saya punya A dan B<br/>
> tolong bantu saya buat C<br/>
> mengikuti pola kombinasi A dan B

perbedaannya:

- kaku → AI menjawab literal, tidak lebih
- natural → AI memahami intent, hasilnya jauh lebih baik

## Case study 1: Request - generate Code dari Gambar

saya punya A: {fileName.html}<br/>
saya punya B: gambar

tolong buatkan untuk saya, C:

- berdasarkan B
- mengikuti pola A

Keterangan:

- **A** = referensi pola/style
- **B** = referensi konten/layout
- **C** = output yang diinginkan

contoh:<br/>
<img src="/Aa_images/web-softwaredeveloperx-com/Request_ke_AI_secara_efektif_dan_efesien__case_study1.png">

## Case study 2: Request - generate Code dari Code yang lain

saya punya A: {fileName.cs}<br/>
saya punya B: {fileName.js}<br/>
saya punya C: {fileName2.cs}<br/>

tolong buatkan untuk saya, D:

- berdasarkan C
- mengikuti pola A dan B

contoh:<br/>
<img src="/Aa_images/web-softwaredeveloperx-com/Request_ke_AI_secara_efektif_dan_efesien__case_study2.png">

## Fine-tune the Tone

Pada situasi tertentu, saya seringkali harus melakukan _fine-tune_ terhadap _tone_ yang sudah saya gunakan.<br/>
Tujuannya untuk mendapatkan _respond_ {dari AI} yang lebih sesuai -- dengan harapan saya.

### Pattern 1 — Visual as Spec

saya punya A: gambar<br/>

tolong buatkan untuk saya, B:

- berdasarkan A

contoh:
> *"convert gambar ini menjadi Fragment HTML"*

Gambar = spec. Tidak perlu describe panjang lebar.

---

### Pattern 2 — Complete, not Create

saya punya A: {file yang sudah ada}<br/>
saya punya B: {referensi}

tolong **lengkapi** A:

- sehingga sesuai dengan B

contoh:
> *"coba tolong lengkapi, sehingga sesuai dengan file .MD tersebut"*

bukan "buatkan dari scratch" — tapi "lengkapi yang sudah ada".<br/>
AI langsung paham konteks dan batasannya.

---

### Pattern 3 — Minimal Bug Report

saya punya A: {screenshot}<br/>

tolong fix:

- bagian yang terlihat "tidak ok"

contoh:
> *"bagian % kurang ok begitu"*

5 kata. AI langsung tahu masalahnya, langsung fix.

---

### Pattern 4 — Scoped Correction

saya punya A: {code snippet}<br/>

tolong jelaskan:

- hanya bagian ini saja
- tidak perlu ubah file apapun

contoh:
> *"tidak usah ubah file .MD, cukup jelaskan bagian ini saja"*

membatasi scope secara eksplisit — AI tidak _over-deliver_.
