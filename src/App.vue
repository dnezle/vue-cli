<template>
  <div id="app" class="container">
    <b-card>
      <b-button-group size="sm">
        <b-button @click="form" :variant="variantForm">Form</b-button>
        <b-button @click="list" :variant="variantList">List</b-button>
      </b-button-group>
      <hr />
      <component :is="ccomponent"></component>
    </b-card>
  </div>
</template>

<script>
import theForm from "./components/TheForm";
import theList from "./components/TheList";

export default {
  name: "App",
  components: {
    theForm,
    theList
  },
  data() {
    return {
      ccomponent: theForm
    };
  },
  computed: {
    variantForm() {
      if (this.ccomponent) {
        return this.ccomponent === theForm ? "primary" : "";
      }
    },
    variantList() {
      if (this.ccomponent) {
        return this.ccomponent === theList ? "primary" : "";
      }
    }
  },
  methods: {
    form() {
      this.ccomponent = theForm;
    },
    list() {
      this.ccomponent = theList;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
