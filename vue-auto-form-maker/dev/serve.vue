<script>
import { defineComponent } from "vue";
import VueAutoFormMaker from "@/vue-auto-form-maker.vue";

export default defineComponent({
  name: "ServeDev",
  components: {
    VueAutoFormMaker,
  },
  data() {
    return {
      testData: [
        { value: "Input1", isMandatory: true },
        { value: "Input2", isMandatory: true },
        { value: "Input3", isMandatory: false },
        { value: "Input4", isMandatory: true },
      ],
      formData: {},
    };
  },
  methods: {
    formSubmit(data) {
      this.formData = data;
    },
  },
});
</script>

<template>
  <div id="app">
    <VueAutoFormMaker @formSubmit="formSubmit" :fieldNames="testData" />
  </div>
</template>
