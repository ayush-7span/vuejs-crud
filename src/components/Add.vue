<template>
  <Header />
  <h1>Hello User,welcome to add component</h1>
  <form class="add">
    <input
      type="text"
      name="name"
      placeholder="Enter your name"
      v-model="restaurent.name"
    />
    <input
      type="text"
      name="contact"
      placeholder="Enter contact number"
      v-model="restaurent.contact"
    />
    <input
      type="text"
      name="address"
      placeholder="Enter your address"
      v-model="restaurent.address"
    />
    <button type="button" v-on:click="addrestaurent">Add new</button>
  </form>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";
export default {
  name: "Add",
  components: {
    Header,
  },
  data() {
    return {
      restaurent: {
        name: "",
        contact: "",
        address: "",
      },
    };
  },
  methods: {
    async addrestaurent() {
      const result = await axios.post("http://localhost:3000/restaurents", {
        name: this.restaurent.name,
        contact: this.restaurent.contact,
        address: this.restaurent.address,
      });
      if (result.status == 201) {
        this.$router.push({ name: "Home" });
      }
    },
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "Signup" });
    }
  },
};
</script>

<style>
</style>