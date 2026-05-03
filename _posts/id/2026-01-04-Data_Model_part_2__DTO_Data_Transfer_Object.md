---
ref: Data_Model_part_2__DTO_Data_Transfer_Object
judul: 'Data Model part 2 - DTO {Data Transfer Object}'
title: 'Data Model part 2 - DTO {Data Transfer Object}'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# Data Model part 2 - DTO {Data Transfer Object}

- Simplicity
    - data dari suatu bagian ke bagian lain
    - data dari suatu Layer ke Layer lainnya
- Security {data sensitivity}
    - dengan pembatasan column
    - dengan _Masking_

<img src="/Aa_images/web-softwaredeveloperx-com/Diagrams/Data-Model--DTO.svg" />

- Entity mapping ke actual `Table`
- DTO akan mapping ke `Database Object` {Table, Views}
- Types {pada FrontEnd} akan mapping ke DTO {pada BackEnd}
- View HTML {pada FrontEnd} akan mapping component HTML ke suatu Object {yang merupakan instance of Types}

**Contoh Implementasi:**

- Table: Sales Order
    - Header dengan lebih dari 80 columns
    - Items dengan lebih dari 50 columns
- Tidak lantas semuanya akan digunakan pada FrontEnd {bagian View HTML} dengan mapping _one to one_
- ada mekanisme:
    - dengan pembatasan column
    - dengan Masking

## Model ada 2 kelompok:

- Model simple
- Model lebih kompleks

## Tipe:

_x._ Database Entity

1. **_blank_**: tanpa suffix
2. **W**: Write-able
3. **R**: Read {W + something Read-able}
4. **X**: Combination {Read + Details}
5. **WD**: Data {W + Data JSON string}
6. **RD**: Data {R + Data JSON string}
7. **\_Details**: untuk Header Details
8. **\_Selection**: untuk pemilihan data di Page: List / Form
9. **\_light**: versi ringkas dari tipe _blank_
10. **\_Item_count**: agregat jumlah item

---

## _x._ Database Entity

merupakan _actual_ `Table` di Database

## 1. **_blank_**: tanpa suffix

- digunakan untuk menampilkan Data
    - di Page: List
    - tidak di Page: Form
- Situasi:
    - Model simple:
        - turunan dari Tipe **W**
    - Model lebih kompleks:
        - karena Tipe **_blank_** ini untuk menampilkan Data, maka perlu melakukan **hide** beberapa field milik Tipe **W**
        - dibuat New _Class_
        - bukan merupakan turunan dari Tipe **W**

```c#
[Framework_Model("XSomethingRequest")]
public class XSomethingRequest
{
    public string Code { get; set; }
    public string StatusX { get; set; }
    // ...
    public double TotalQuantity { get; set; }
    public double TotalOpenQuantity { get; set; }
    // field yang spesifik untuk keperluan List
}
```

## 2. **W**: Write-able

- digunakan untuk _Write_ data ke _Entity_ di Database
- dibuat beda dengan _Entity_, karena ada beberapa _field_ milik Entity yang perlu di _hide_
- sering diperlukan cara "Aliasing", maka digunakan keyword:

```
[Computed]
[JsonIgnore]
```

- contoh Aliasing:

```c#
[Computed]
[JsonIgnore]
public virtual string VendorID
{
    get { return Vendor; }
}

public string Vendor { get; set; }
```

> **Note:** pattern ini digunakan untuk mapping field name antara Entity vs sistem eksternal, tanpa expose kedua nama sekaligus ke FrontEnd.

## 3. **R**: Read {W + something Read-able}

- digunakan untuk _Read_ data pada Page: Form
- turunan dari Tipe **W**
- ditambahkan beberapa kolom/field untuk Informasi tambahan
    - dengan pola suffix `X` pada fieldName, untuk label / display name

```c#
[Framework_Model("XSomethingRequestR")]
public class XSomethingRequestR : XSomethingRequestW
{
    public DateTime InsertStamp { get; set; }
    public string InsertedBy { get; set; }
    public string VendorX { get; set; }        // display name untuk Vendor
    public string StatusX { get; set; }        // display name untuk Status
    // ...
}
```

## 4. **X**: Combination {Read + Details}

- kita memerlukan Tipe ini, untuk Model yang bersifat Header - Detail
- ada bagian "Header" → `dataInput`
- ada bagian "Details" → `details`

```c#
public class XSomethingRequestX
{
    // note:
    //    - untuk konsisten dengan FrontEnd
    //    - maka huruf kecil dataInput, dan bukan DataInput
    //    - berlaku juga untuk details
    public XSomethingRequestWD dataInput { get; set; }
    public XSomethingRequest_Details details { get; set; }
}
```

## 5. **WD**: Data {W + Data JSON string}

- Tipe ini diperlukan untuk handle kolom Data {String JSON}
    - turunan dari Tipe **W**
    - nantinya berisi data/content yang cukup besar
    - dibuat kelas terpisah:
        - suatu waktu kolom Data {String JSON} ini, bisa dipindah ke Database yang lain {untuk keperluan Performance}
        - maka Class ini menjadi mudah untuk diubah

```c#
public class XSomethingRequestWD : XSomethingRequestW
{
    public string Data { get; set; }
}
```

## 6. **RD**: Data {R + Data JSON string}

- sama seperti **WD**, tetapi turunan dari Tipe **R**
- digunakan ketika Form perlu menampilkan data lengkap beserta JSON string

```c#
[Framework_Model("XSomethingRequestR")]
public class XSomethingRequestRD : XSomethingRequestR
{
    public string Data { get; set; }
}
```

> **Note:** `[Framework_Model]` pada RD menggunakan nama yang sama dengan **R** — karena RD merupakan superset dari R.

## 7. **\_Details**: untuk Header Details

- Class untuk Details
- berisi 1 atau lebih Array
- contoh:

```c#
public class XSomethingRequest_Details
{
    public XSomethingRequestItemW[] Items { get; set; }
}
```

```c#
// contoh lebih kompleks:
public class XSomethingElse_Details
{
    public XSomethingRequestItemW[] Items { get; set; }
    public XExpense[] Expenses { get; set; }
    // ...
}
```

## 8. **\_Selection**: untuk pemilihan data

- digunakan untuk menampilkan data dalam konteks _selection_ / _lookup_
    - biasanya berupa modal / dialog pilih data
    - bisa juga expandable row di Page: List
- bukan untuk Write
- naming convention: `{Entity}_Selection` atau `{Entity}_{DetailName}_Selection`
- contoh:

```c#
[Framework_Model("XSomethingRequestItem_Selection")]
public class XSomethingRequestItem_Selection
{
    public string RequestCode { get; set; }
    public string ItemCode { get; set; }
    public string Description { get; set; }
    // ... field yang relevan untuk tampilan selection
    public double TotalOpenQuantity { get; set; }
}
```

## 9. **\_light**: versi ringkas dari _blank_

- inherit dari tipe **_blank_**, tanpa penambahan field
- digunakan ketika perlu Class name yang berbeda untuk keperluan `[Framework_Model]`
    - misalnya: untuk endpoint atau context yang berbeda
- contoh:

```c#
[Framework_Model("XSomethingRequest_light")]
public class XSomethingRequest_light : XSomethingRequest { }
```

> **Note:** Meskipun Class-nya kosong, `[Framework_Model]` yang berbeda memungkinkan Framework melakukan mapping secara terpisah.

## 10. **\_Item_count**: agregat jumlah item

- Class sederhana untuk menampilkan jumlah item per record
- biasanya digunakan untuk keperluan UI: badge / counter di Page: List
- contoh:

```c#
[Framework_Model("XSomethingRequest_Item_count")]
public class XSomethingRequest_Item_count
{
    public string Code { get; set; }
    public int Count { get; set; }
}
```

---

## Catatan:

- pada coding, untuk lebih mudah dibaca — Model Tipe **W** biasanya ditulis terlebih dahulu, daripada Tipe **_blank_**
- simple `CoC: Convention over Configuration`:
    - suffix `X` pada nama field (bukan nama Class) = display name / label untuk field tersebut<br/>
      contoh:
        - `StatusX` untuk `Status`
        - `VendorX` untuk `Vendor`
    - manfaat: mempermudah pada FrontEnd

mengapa saya menggunakan **suffix** `X`?

- X = singkatan dari e**X**tended / e**X**tra
    - `StatusX` → _extended info_ dari `Status`
    - `VendorX` → _extra info_ dari `Vendor`
- praktis:
    - pendek — hanya 1 karakter
    - tidak konflik dengan nama field yang umum

> suffix `X` = display name / label untuk field tersebut

**alternatif yang dipertimbangkan — dan kenapa tidak dipilih:**

- suffix `Label` → terlalu panjang: `StatusLabel`
- suffix `Name` → ambigu: `StatusName` bisa salah diartikan
- suffix `Display` → verbose: `StatusDisplay`

> `X` menang karena: singkat, konsisten, dan maknanya jelas setelah terbiasa

### keyword:

- `[Table]` → mapping ke nama Table di Database
    - contoh: `[Table("Table_Name")]`
- `[Framework_Model]` → mapping ke nama Model di Framework
    - contoh: `[Framework_Model("XPROD_ViewName")]`
- `[ExplicitKey]` → Primary Key yang tidak auto-generate
- `[Computed]` dan `[JsonIgnore]` → field yang tidak dikirim ke FrontEnd, digunakan untuk Aliasing
