<template>
  <div class="q-pa-md" id="container">
    <q-table
      grid
      title="Employees"
      :title-class="'text-h2'"
      :rows="rows"
      :columns="columns"
      row-key="name"
      :filter="filter"
      card-class="bg-grey-8 text-white"
      :rows-per-page-options="[0]"
      :pagination="pagination"
    >
      <template v-slot:top-right>
        <q-input
          class="filter-search"
          borderless
          dense
          debounce="100"
          v-model="filter"
          placeholder="Search"
        >
          <template v-slot:append>
            <q-icon name="search" />
          </template>
        </q-input>
      </template>
    </q-table>
  </div>
</template>

<script>
import { ref } from "vue";
import api from "../services/api";

const columns = [
  {
    name: "nome",
    required: true,
    label: "Nome",
    align: "left",
    field: (row) => row.name,
    format: (val) => `${val}`,
  },
  { name: "username", align: "center", label: "UserName", field: "username" },
  { name: "phone", label: "Phone", field: "phone" },
  { name: "email", label: "Email", field: "email" },
  { name: "website", label: "Website", field: "website" },
  { name: "company", label: "Company", field: (row) => row.company.name },
  { name: "company", label: "Catch Phrase", field: (row) => row.company.catchPhrase },
  { name: "address", label: "Address", field: (row) => row.address.street },
  { name: "address", label: "City", field: (row) => row.address.city },
  { name: "address", label: "Suite", field: (row) => row.address.suite },
];

const rows = [
  {
    name: "",
    username: "",
    phone: "",
    email: "",
    website: "",
    address: {
      street: "",
      suite: "",
      city: "",
    },
    company: {
      name: "",
      catchPhrase: "",
    },
  },
];

export default {

  data() {
    return {
      filter: ref(""),
      columns,
      rows,
      pagination: {
        page: 1,
        rowsPerPage: 0,
      },
    };
  },

  mounted() {
    api.get("").then((res) => {
      this.rows = res.data;
      console.log(res);
    });
  },
};
</script>

<style scoped>
#container {
  width: 100%;
  height: 100vh;
  display: flex;
  align-content: center;
  justify-items: center;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
}
.filter-search {
  width: 320px;
  background-color: aliceblue;
  padding: 10px;
  border-radius: 10px;
  margin: 30px 0 15px 0;
}
.cardInfo {
  background-color: gray;
}

</style>
