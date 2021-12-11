<script>
import { defineComponent } from "vue";

export default /*#__PURE__*/ defineComponent({
  name: "VueAutoFormMaker", // vue component name
  data() {
    return {
      fields: [],
      inputData: [],
      models: null,
      error: {
        msg: "",
      },
    };
  },
  created() {
    console.log(this.$props.inputFields);
    this.fields = this.$props.inputFields;
    this.fields.forEach((element, index) => {
      this.inputData[index] = {
        placeholder: this.toCapitalizedStr(element.value),
        vmodel: element.value.replace(/\s/g, "").toLowerCase(),
        isMandatory: element.isMandatory,
        error: false,
      };
      this.models = { ...this.models, [this.inputData[index].vmodel]: "" };
    });
  },
  methods: {
    toCapitalizedStr(str) {
      return str
        .split(" ")
        .map(function (word, index) {
          // If it is the first word make sure to lowercase all the chars.
          if (index == 0) {
            return word.charAt(0).toUpperCase() + word.slice(1).toLowerCase();
          }
          // If it is not the first word only upper case the first char and lowercase the rest.
          return word.charAt(0).toUpperCase() + word.slice(1).toLowerCase();
        })
        .join(" ");
    },
    validateForm() {
      var res = false;
      for (let index = 0; index < this.inputData.length; index++) {
        this.inputData[index].error = false;
        if (this.inputData[index].isMandatory) {
          if (
            this.models[this.inputData[index].vmodel] == null ||
            this.models[this.inputData[index].vmodel] == ""
          ) {
            this.inputData[index].error = true;
            this.error.msg = "Please fill out " + this.inputData[index].vmodel;
            return;
          }
        }

        res = true;
      }
      if (res) {
        //Emit to outer world
        this.error.msg = "";
        this.$emit("formSubmit", this.models);
      }
    },
  },
  props: {
    buttonText: {
      type: String,
      default: "Submit",
    },
    showButton: {
      type: Boolean,
      default: true,
    },
    wrapperClass: {
      type: String,
      default: "afm-form-wrapper",
    },
    inputClass: {
      type: String,
      default: "afm-field-class",
    },
    btnClass: {
      type: String,
      default: "afm-btn-class afm-outlined",
    },
    inputFields: {
      type: Array,
      default: [{ value: "Username", isMandatory: true }],
    },
    errorClass: {
      type: String,
      default: "afm-error-input",
    },
  },
});
</script>

<template>
  <div :class="wrapperClass">
    <div v-for="(field, index) in inputData" :key="index">
      <input
        :class="[this.inputData[index].error ? errorClass : '', inputClass]"
        :placeholder="field.placeholder"
        v-model="models[field.vmodel]"
      />
    </div>
    <button @click="validateForm" :class="btnClass" v-show="showButton">
      {{ buttonText }}
    </button>
    <div>
      {{ error.msg }}
    </div>
  </div>
</template>

<style scoped>
.afm-form-wrapper {
  padding: 1rem 0.5rem 1rem 0.2rem;
  -webkit-box-shadow: 0 2px 1px -1px rgb(0 0 0 / 20%),
    0 1px 1px 0 rgb(0 0 0 / 14%), 0 1px 3px 0 rgb(0 0 0 / 12%);
  box-shadow: 0 2px 1px -1px rgb(0 0 0 / 20%), 0 1px 1px 0 rgb(0 0 0 / 14%),
    0 1px 3px 0 rgb(0 0 0 / 12%);
  border-radius: 1%;
  margin-bottom: 2rem;
  flex-direction: column;
  display: flex;
  margin: 0;
  align-items: center;
}
.afm-auto-form-maker p {
  margin: 0 0 1em;
}

.afm-field-class {
  margin: 0.5rem;
}

.afm-btn-class {
  padding-inline: 3.6rem;
  padding-block: 0.3rem;
  margin-block-start: 1rem;
}

.afm-outlined {
  background: none;
  border: 1px solid black;
}

.afm-error-input {
  border-color: red;
}
</style>
