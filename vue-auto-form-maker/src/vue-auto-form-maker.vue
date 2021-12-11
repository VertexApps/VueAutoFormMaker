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
  mounted() {
    this.fields = this.$props.fieldNames;
    this.fields.forEach((element, index) => {
      this.inputData[index] = {
        placeholder: this.toCapitalizedStr(element.value),
        vmodel: element.value.replace(/\s/g, "").toLowerCase(),
        isMandatory: element.isMandatory,
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
        if (this.inputData[index].isMandatory) {
          if (
            this.models[this.inputData[index].vmodel] == null ||
            this.models[this.inputData[index].vmodel] == ""
          ) {
            this.error.msg =
              "Please fill out " + this.inputData[index].placeholder;
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
    fieldNames: {
      type: Array,
      default: [{ value: "Username", isMandatory: true }],
    },
  },
});
</script>

<template>
  <div :class="wrapperClass">
    <div v-for="(field, index) in inputData" :key="index">
      <input
        :class="inputClass"
        :placeholder="field.vmodel"
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
  display: block;
  width: 400px;
  margin: 25px auto;
  border: 1px solid #ccc;
  border-radius: 10px;
  text-align: center;
  padding: 25px;
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
</style>
