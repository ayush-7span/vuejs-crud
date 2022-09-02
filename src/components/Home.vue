<template>
  <Header />
  <h1>hello {{ name }} welcome to Home Page</h1>
  <table border="2">
    <tr>
      <td>id</td>
      <td>name</td>
      <td>contact</td>
      <td>address</td>
      <td>actions</td>
    </tr>
    <tr v-for="item in restaurents" :key="item.id">
      <td>{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.contact }}</td>
      <td>{{ item.address }}</td>
       <td>
        <router-link :to="'/update/' + item.id">Update</router-link>
        <button v-on:click="deleterestaurent(item.id)">Delete</button>
      </td>
    </tr>
  </table>
</template>
<script>
import Header from "../components/Header.vue";
import axios from "axios";
export default {
  name: "Home",
  data() {
    return {
      name: "",
      restaurents: [],
    };
  },
  components: {
    Header,
  },
  methods: {
    async deleterestaurent(id) {
      let result = await axios.delete(
        "http://localhost:3000/restaurents/" + id
      );
      if (result.status == 200) {
        this.loadData();
      }
    },
    async loadData() {
      let user = localStorage.getItem("user-info");
      this.name = JSON.parse(user)[0].name;
      if (!user) {
        this.$router.push({ name: "Signup" });
      }
      let result = await axios.get("http://localhost:3000/restaurents");
      this.restaurents = result.data;
    },
  },
  async mounted() {
    this.loadData();
  },
};
</script>
<style>
td {
  width: 160px;
  height: 25px;
}
</style>
