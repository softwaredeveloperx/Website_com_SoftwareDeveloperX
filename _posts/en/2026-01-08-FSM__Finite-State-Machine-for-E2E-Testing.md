---
ref: FSM__Finite-State-Machine-for-E2E-Testing
judul: 'FSM: Finite State Machine for E2E {end-to-end} Testing'
title: 'FSM: Finite State Machine for E2E {end-to-end} Testing'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# FSM: Finite State Machine for E2E {end-to-end} Testing

My experience using `Playwright` for E2E {end-to-end} Testing across many Forms:

- the `page.waitForTimeout()` function works reasonably well for some situations
- but when a `FrontEnd` section performs several `fetch` calls in a _cascade_ == a different story entirely
- I needed a consistent mechanism
- I had to build "a Pattern" that is _robust_ for E2E {end-to-end} Testing

## FSM: concept in a `JavaScript` file

```js
// example implementation — can be adapted to any framework
page_Kondisi = 'unknown' // [unknown, prepare, ready, processing, data_exist, data_not_found, data_error, validation_error, submit_data, submit_error, submit_success]
still_processing = false
page_Message = ''

/*
Page State:

┌─────────────┐
│   prepare   │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│ processing  │ ◄─── Loading data
└──────┬──────┘
       │
       ├─────► data References
       ├─────► {show existing Data}
       ├──────────► data_exist
       ├──────────► data_not_found
       ├──────────► data_error
       │
       ▼
┌─────────────┐
│    ready    │ ◄─── User can interact
└──────┬──────┘
       │
       ▼
┌─────────────┐
│ submit_data │ ◄─── User clicked button [Save, Submit, Verify, ...]
└──────┬──────┘
       │
       ├─────► validation_error
       ├─────► submit_error
       └─────► submit_success

*/
```

## FSM: Implementation

We can implement this FSM concept using any commonly used `JavaScript Framework/Library`. For now, I chose `VUE` as follows:

```
<script setup>
import Global_Data_APP from '@app/helpers/Global_Data_APP'

const route = useRoute()
const { sdr_GoBack } = useSdrGoBack()
const dataRefs = reactive({})

dataRefs.page_Kondisi = 'unknown' // [unknown, prepare, ready, processing, data_exist, data_not_found, data_error, validation_error, submit_data, submit_error, submit_success]
dataRefs.still_processing = false
dataRefs.page_Message = ''

// this is for UI {handle proper CSS}
dataRefs.form_submitted = false

/*
Page State:

┌─────────────┐
│   prepare   │
└──────┬──────┘
        │
        ▼
┌─────────────┐
│ processing  │ ◄─── Loading data
└──────┬──────┘
        │
        ├─────► data References
        ├─────► {show existing Data}
        ├──────────► data_exist
        ├──────────► data_not_found
        ├──────────► data_error
        │
        ▼
┌─────────────┐
│    ready    │ ◄─── User can interact
└──────┬──────┘
        │
        ▼
┌─────────────┐
│ submit_data │ ◄─── User clicked button [Save, Submit, Verify, ...]
└──────┬──────┘
        │
        ├─────► validation_error
        ├─────► submit_error
        └─────► submit_success

*/

// CRUD: Create, Read, Update, Delete
dataRefs.Is_Read = false
dataRefs.Is_Create = false
dataRefs.Is_Update = false
dataRefs.Is_Writeable = false

let model_Template = {
    Code: '',
    Description: '',
    Active: true,
}

dataRefs.model = { ...model_Template }

// some Functions
async function showData() {
    if (!dataRefs.Is_Read) return true

    Global_Data_APP.setProcessing(dataRefs, true, 'processing')
    let response = await Global_Data_APP.dataSingle('XSomethingR', dataRefs.model.Code)

    if (!response.success) {
        Global_Data_APP.setProcessing(dataRefs, false, 'data_error')

        dataRefs.page_Message = response.data

        return false
    }

    if (!response.data) {
        let code = dataRefs.model.Code

        // reset
        dataRefs.model = { ...model_Template }

        dataRefs.page_Message = `Data with code '${code}' was not found`
        Global_Data_APP.messageValidasi(dataRefs.page_Message)

        Global_Data_APP.setProcessing(dataRefs, false, 'data_not_found')

        return false
    }

    dataRefs.model = response.data

    Global_Data_APP.setProcessing(dataRefs, false, 'data_exist')

    return true
}

async function saveData(skipConfirmation = false) {
    if (dataRefs.still_processing) return

    dataRefs.form_submitted = true
    Global_Data_APP.setProcessing(dataRefs, true, 'submit_data')

    if (!(await Valid_toSave(skipConfirmation))) {
        Global_Data_APP.setProcessing(dataRefs, false, 'validation_error')

        return
    }

    let data = {
        dataInput: {
            ...dataRefs.model,
        },
    }

    Global_Data_APP.SanitizeInput(data, model_Template)

    let response = await Global_Data_APP.dataSave(data.dataInput, dataRefs.Is_Create, 'Something')

    if (!response.success) {
        Global_Data_APP.setProcessing(dataRefs, false, 'submit_error')
        dataRefs.form_submitted = false

        dataRefs.page_Message = response.data

        Global_Data_APP.messageError(dataRefs.page_Message)

        return
    }

    // - Loading remains true
    // - page_Kondisi is changed to 'submit_success'
    Global_Data_APP.setProcessing(dataRefs, true, 'submit_success')

    // - here, Loading is changed to false
    Global_Data_APP.messageInfo(dataRefs, 'Data saved successfully', () => sdr_GoBack())
}

async function Valid_toSave(skipConfirmation) {
    dataRefs.page_Message = ''

    const modelChecks = [{ field: 'Description', msg: 'Name must not be empty' }]

    let x = await Global_Data_APP.Valid_toSave_all(dataRefs, modelChecks)
    if (!x) return x

    return true
}

async function Data_References() {
    if (!dataRefs.Is_Writeable) return

    Global_Data_APP.setProcessing(dataRefs, true, 'processing')

    Global_Data_APP.setProcessing(dataRefs, false)
}

async function Set_Editable() {
    if (dataRefs.still_processing) return

    dataRefs.Is_Read = false
    dataRefs.Is_Create = false
    dataRefs.Is_Update = true

    dataRefs.Is_Writeable = dataRefs.Is_Create || dataRefs.Is_Update

    Data_References()
}

function handleParameters() {
    dataRefs.model.Code = Global_Data_APP.Simple_Decode(route.query.code || '')

    dataRefs.Is_Read = Global_Data_APP.Not_Null(dataRefs.model.Code)

    dataRefs.Is_Create = !dataRefs.Is_Read
    dataRefs.Is_Update = false

    dataRefs.Is_Writeable = dataRefs.Is_Create || dataRefs.Is_Update
}

async function initialize_Page() {
    dataRefs.page_Kondisi = 'prepare'

    handleParameters()

    await Data_References()

    if (!(await showData())) return

    dataRefs.page_Kondisi = 'ready'
}

useWatchPageInformation(dataRefs)

let isFirstMount = true

onMounted(async () => {
    await initialize_Page()
    isFirstMount = false
})

watch(
    () => route.fullPath,
    async () => {
        if (isFirstMount) return
        await initialize_Page()
    },
)
</script>

<template>
    <div class="w-100 flex-grow-1" :class="{ sedangSubmitForm: dataRefs.form_submitted, 'sdr-mode-read': !dataRefs.Is_Writeable }">
        <div class="card">
            <div class="card-header d-flex align-items-center">
                <i class="fa fa-edit me-2"></i>
                <strong>Form: Something</strong>
            </div>
            <div class="card-body">
                <div class="sdr_Toolbar">
                    <div class="d-flex align-items-center gap-2">
                        <button class="sdr_button sdr_button_y" @click="() => Set_Editable()" v-if="!dataRefs.Is_Writeable"><CIcon icon="cilSave" /> Edit</button>
                        <button class="sdr_button sdr_button_b" @click="saveData" v-if="dataRefs.Is_Writeable"><CIcon icon="cil-check-circle" /> Save</button>
                        <div class="pull-left" style="width: 50px; text-align: center; padding-top: 5px" v-show="dataRefs.still_processing"><i class="fa fa-spinner fa-spin" style="font-size: 24px; display: none" id="idLoading"></i>&nbsp;</div>
                        <button class="sdr_button ms-auto" @click="sdr_GoBack"><i class="fa fa-sign-out"></i> Cancel</button>
                    </div>
                </div>
                <div class="row g-3">
                    <div class="col-12 col-md-3">
                        <label class="form-label">Code</label>
                        <input type="text" class="form-control form-control-sm" data-field="Code" v-model="dataRefs.model.Code" :readonly="!dataRefs.Is_Create" :class="{ 'sdr-hanya-tulis-1-kali': !dataRefs.Is_Create }" placeholder="e.g. DIV-001" />
                    </div>
                    <div class="col-12 col-md-5">
                        <label class="form-label"> Name <span class="text-danger">*</span> </label>
                        <input type="text" class="form-control form-control-sm" :class="{ 'is-invalid': dataRefs.form_submitted && !dataRefs.model.Description }" data-field="Description" v-model="dataRefs.model.Description" :readonly="!dataRefs.Is_Writeable" placeholder="e.g. Business" />
                    </div>
                </div>
                <div class="row g-3 mt-1">
                    <div class="col-12 col-md-3">
                        <label class="form-label">Status</label>
                        <div class="d-flex align-items-center gap-2">
                            <div class="form-check form-switch">
                                <input type="checkbox" class="form-check-input" role="switch" data-field="Active" v-model="dataRefs.model.Active" :disabled="!dataRefs.Is_Writeable" style="width: 3em; height: 1.5em" />
                            </div>
                            <span>{{ dataRefs.model.Active ? 'Active' : 'Inactive' }}</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

```
