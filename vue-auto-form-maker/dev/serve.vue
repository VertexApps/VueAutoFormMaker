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
        { value: "Username", isMandatory: true },
        { value: "Password", isMandatory: true },
        { value: "Email", isMandatory: false },
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
    <VueAutoFormMaker @formSubmit="formSubmit" :inputFields="testData" />
  </div>
</template>
