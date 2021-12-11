# vue-auto-form-maker

> This is a very early version - updates will follow

![Alt Text](https://media.giphy.com/media/waX1f2hb7hbXNGgMUj/giphy.gif)

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
    <VueAutoFormMaker :inputFields="testData" />
  </div>
</template>

<script>
import VueAutoFormMaker from "@/vue-auto-form-maker.vue";

export default({
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

## Props

Submit Button:

- buttonText: text of the Submit button ( String , "Submit" )
- showButton: Show or hide the submit button (Bool,true)

Css Classes:

- wrapperClass: Css class for the form Wrapper (String,'afm-form-wrapper')
- inputClass: CSS class of the individual input field(String,'afm-field-class')
- inputClass: CSS class of the individual input field(String,'afm-field-class')
- btnClass: CSS class of the submit button
- errorClass: CSS class of the error state

Input fields:

- inputFields: Object containing the data for each field

```js
 inputFields: [
        { value: "Input1", isMandatory: true },
        { value: "Input2", isMandatory: true },
        { value: "Input3", isMandatory: false },
        { value: "Input4", isMandatory: true },
      ],
```

## Events

- @formSubmit - called when the submit button is pressed, will return an object with all the data

```js
 methods: {
    formSubmit(data) {
      //Do what you want with data from the from
      //Data will contain:
      //{input1:'inputValue',input2:'inputValue'....}
    },
  },
```

## Change Log

V0.0.8 - Added support for custom error css

## License

Copyright (c) 2021 [Valeri Shnaider](https://github.com/VertexApps). Released under the [MIT license]
