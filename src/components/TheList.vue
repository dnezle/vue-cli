<template>
  <b-card header="Lists">
    <b-table
      hover
      bordered
      small
      :sort-by.sync="sortBy"
      :sort-desc.sync="sortDesc"
      :items="items"
      :fields="field"
      v-if="items.length"
    >
      <template slot="action" slot-scope="row" size="sm">
        <b-button size="sm" variant="primary">Edit</b-button>
        <b-button @click="remove(row.item);" size="sm" variant="danger"
          >Delete</b-button
        >
      </template>
    </b-table>
    <b-alert v-if="!items.length" variant="warning"
      >No records to be displayed</b-alert
    >
  </b-card>
</template>

<script>
export default {
  data() {
    return {
      sortBy: "age",
      sortDesc: false,
      field: [
        { key: "name", label: "Name" },
        { key: "age", label: "Age", sortable: true },
        { key: "action", label: "Action" }
      ],
      items: []
    };
  },
  methods: {
    remove(row) {
      this.items.splice(row, 1);
    }
  },
  created() {
    this.items = JSON.parse(localStorage.getItem("Persons"));
  }
};
</script>
