<template>
  <b-card header="Form">
    <transition name="fade">
      <b-alert :show="successMsg" dismissible variant="success"
        >Successfully Saved!.</b-alert
      >
    </transition>
    <b-form-group horizontal size="sm" label="Name:">
      <b-form-input
        horizontal
        size="sm"
        v-model="formData.name"
        :state="!$v.formData.name.$invalid"
      ></b-form-input>
      <div v-if="!$v.formData.name.required">Must not be empty!.</div>
    </b-form-group>
    <b-form-group horizontal size="sm" label="Age:">
      <b-form-input
        horizontal
        size="sm"
        v-model="formData.age"
        :state="!$v.formData.age.$invalid"
      ></b-form-input>
      <div v-if="!$v.formData.age.required">Must not be empty!.</div>
      <div v-if="!$v.formData.age.numeric">Must be numeric</div>
    </b-form-group>
    <b-button
      @click="submit"
      size="sm"
      variant="success"
      :disabled="$v.formData.$invalid"
      >Submit</b-button
    >
  </b-card>
</template>

<script>
import { required, numeric } from "vuelidate/lib/validators";
export default {
  data() {
    return {
      formData: [{ name: null }, { age: null }],
      persons: [],
      successMsg: 0
    };
  },
  methods: {
    submit() {
      this.persons.push({
        name: this.formData.name,
        age: this.formData.age
      });
      localStorage.setItem("Persons", JSON.stringify(this.persons));
      setTimeout(() => {
        this.successMsg = true;
        this.formData = [];
      }, 1000);
    }
  },
  created() {
    this.persons = JSON.parse(localStorage.getItem("Persons"));
  },
  validations: {
    formData: {
      name: {
        required
      },
      age: {
        required,
        numeric
      }
    }
  }
};
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 2s ease-out;
}
</style>
