# vue-auto-form-maker

> This is a very early version

This package lets you create a dynamic form with validation and customizable css classes

## Installation

```bash
npm install vue-auto-form-maker
```

## Usage - Gloabl

```js
//main.js file
import VueAutoFormMaker from "@/vue-auto-form-maker.vue";

//register the Component to use it Globally
app.component("VueAutoFormMaker", VueAutoFormMaker);
```

## Usage - Local

```js
<template>
  <div id="app">
    <VueAutoFormMaker @formSubmit="formSubmit" :fieldNames="testData" />
  </div>
</template>

<script>
//Import VueAutoFormMaker into your View
import VueAutoFormMaker from "@/vue-auto-form-maker.vue";

export default defineComponent({
  name: "ServeDev",
  components: {
    VueAutoFormMaker,
  },
  data() {
    return {
      //Define your input fields
      testData: [
        { value: "Input1", isMandatory: true },
        { value: "Input2", isMandatory: true },
        { value: "Input3", isMandatory: false },
        { value: "Input4", isMandatory: true },
      ],
    };
  },
  methods: {
    formSubmit(data) {
      //Do what you want with data from the from
    },
  },
});
</script>
```
