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
    - data flows from one part to another
    - data flows from one Layer to another
- Security {data sensitivity}
    - column restriction
    - _Masking_

<img src="/Aa_images/web-softwaredeveloperx-com/Diagrams/Data-Model--DTO.svg" />

- Entity maps to the actual `Table`
- DTO maps to `Database Object` {Table, Views}
- Types {on the FrontEnd} map to DTO {on the BackEnd}
- HTML View {on the FrontEnd} maps HTML components to an Object {which is an instance of Types}

**Implementation Example:**

- Table: Sales Order
    - Header with more than 80 columns
    - Items with more than 50 columns
- Not everything will be used on the FrontEnd {HTML View} with a _one to one_ mapping
- there are mechanisms for:
    - column restriction
    - Masking

## Model has 2 groups:

- Simple Model
- More complex Model

## Types:

_x._ Database Entity

1. **_blank_**: no suffix
2. **W**: Write-able
3. **R**: Read {W + something Read-able}
4. **X**: Combination {Read + Details}
5. **WD**: Data {W + Data JSON string}
6. **RD**: Data {R + Data JSON string}
7. **\_Details**: for Header Details
8. **\_Selection**: for data selection on Page: List / Form
9. **\_light**: a compact version of the _blank_ type
10. **\_Item_count**: aggregate item count

---

## _x._ Database Entity

represents the _actual_ `Table` in the Database

## 1. **_blank_**: no suffix

- used to display Data
    - on Page: List
    - not on Page: Form
- Situation:
    - Simple Model:
        - inherits from Type **W**
    - More complex Model:
        - since this **_blank_** Type is for displaying Data, some fields from Type **W** need to be **hidden**
        - a new _Class_ is created
        - does not inherit from Type **W**

```c#
[Framework_Model("XSomethingRequest")]
public class XSomethingRequest
{
    public string Code { get; set; }
    public string StatusX { get; set; }
    // ...
    public double TotalQuantity { get; set; }
    public double TotalOpenQuantity { get; set; }
    // fields specific to List page needs
}
```

## 2. **W**: Write-able

- used to _Write_ data to an _Entity_ in the Database
- kept separate from the _Entity_, because some Entity fields need to be _hidden_
- "Aliasing" is often needed, so the following keywords are used:

```
[Computed]
[JsonIgnore]
```

- Aliasing example:

```c#
[Computed]
[JsonIgnore]
public virtual string VendorID
{
    get { return Vendor; }
}

public string Vendor { get; set; }
```

> **Note:** this pattern is used to map field names between the Entity and an external system, without exposing both names to the FrontEnd at the same time.

## 3. **R**: Read {W + something Read-able}

- used to _Read_ data on Page: Form
- inherits from Type **W**
- additional columns/fields are added for supplementary information
    - using the suffix `X` pattern on fieldName, for label / display name

```c#
[Framework_Model("XSomethingRequestR")]
public class XSomethingRequestR : XSomethingRequestW
{
    public DateTime InsertStamp { get; set; }
    public string InsertedBy { get; set; }
    public string VendorX { get; set; }        // display name for Vendor
    public string StatusX { get; set; }        // display name for Status
    // ...
}
```

## 4. **X**: Combination {Read + Details}

- this Type is needed for Models that follow a Header - Detail structure
- there is a "Header" part → `dataInput`
- there is a "Details" part → `details`

```c#
public class XSomethingRequestX
{
    // note:
    //    - for consistency with the FrontEnd
    //    - use lowercase dataInput, not DataInput
    //    - same applies to details
    public XSomethingRequestWD dataInput { get; set; }
    public XSomethingRequest_Details details { get; set; }
}
```

## 5. **WD**: Data {W + Data JSON string}

- this Type is needed to handle a Data column {JSON String}
    - inherits from Type **W**
    - will eventually hold fairly large data/content
    - created as a separate class:
        - at some point, this Data column {JSON String} could be moved to a different Database {for Performance reasons}
        - making this Class easy to modify

```c#
public class XSomethingRequestWD : XSomethingRequestW
{
    public string Data { get; set; }
}
```

## 6. **RD**: Data {R + Data JSON string}

- same as **WD**, but inherits from Type **R**
- used when a Form needs to display the complete data including the JSON string

```c#
[Framework_Model("XSomethingRequestR")]
public class XSomethingRequestRD : XSomethingRequestR
{
    public string Data { get; set; }
}
```

> **Note:** `[Framework_Model]` on RD uses the same name as **R** — because RD is a superset of R.

## 7. **\_Details**: for Header Details

- Class for Details
- contains 1 or more Arrays
- example:

```c#
public class XSomethingRequest_Details
{
    public XSomethingRequestItemW[] Items { get; set; }
}
```

```c#
// more complex example:
public class XSomethingElse_Details
{
    public XSomethingRequestItemW[] Items { get; set; }
    public XExpense[] Expenses { get; set; }
    // ...
}
```

## 8. **\_Selection**: for data selection

- used to display data in a _selection_ / _lookup_ context
    - typically a modal / dialog for selecting data
    - can also be an expandable row on Page: List
- not for Write
- naming convention: `{Entity}_Selection` or `{Entity}_{DetailName}_Selection`
- example:

```c#
[Framework_Model("XSomethingRequestItem_Selection")]
public class XSomethingRequestItem_Selection
{
    public string RequestCode { get; set; }
    public string ItemCode { get; set; }
    public string Description { get; set; }
    // ... fields relevant for the selection display
    public double TotalOpenQuantity { get; set; }
}
```

## 9. **\_light**: compact version of _blank_

- inherits from the **_blank_** type, without adding any fields
- used when a different Class name is needed for `[Framework_Model]`
    - for example: for a different endpoint or context
- example:

```c#
[Framework_Model("XSomethingRequest_light")]
public class XSomethingRequest_light : XSomethingRequest { }
```

> **Note:** Even though the Class is empty, a different `[Framework_Model]` allows the Framework to handle the mapping separately.

## 10. **\_Item_count**: aggregate item count

- a simple Class to display the number of items per record
- typically used for UI purposes: badge / counter on Page: List
- example:

```c#
[Framework_Model("XSomethingRequest_Item_count")]
public class XSomethingRequest_Item_count
{
    public string Code { get; set; }
    public int Count { get; set; }
}
```

---

## Notes:

- in coding, for readability — Type **W** Model is usually written first, before the **_blank_** Type
- simple `CoC: Convention over Configuration`:
    - suffix `X` on the field name (not the Class name) = display name / label for that field<br/>
      examples:
        - `StatusX` for `Status`
        - `VendorX` for `Vendor`
    - benefit: makes things easier on the FrontEnd

why do I use the **suffix** `X`?

- X = short for e**X**tended / e**X**tra
    - `StatusX` → _extended info_ from `Status`
    - `VendorX` → _extra info_ from `Vendor`
- practical:
    - short — only 1 character
    - no conflict with common field names

> suffix `X` = display name / label for that field

**alternatives considered — and why they were not chosen:**

- suffix `Label` → too long: `StatusLabel`
- suffix `Name` → ambiguous: `StatusName` could be misread
- suffix `Display` → verbose: `StatusDisplay`

> `X` wins because: short, consistent, and its meaning is clear once you're used to it

### keywords:

- `[Table]` → maps to the Table name in the Database
    - example: `[Table("Table_Name")]`
- `[Framework_Model]` → maps to the Model name in the Framework
    - example: `[Framework_Model("XPROD_ViewName")]`
- `[ExplicitKey]` → Primary Key that is not auto-generated
- `[Computed]` and `[JsonIgnore]` → fields not sent to the FrontEnd, used for Aliasing
