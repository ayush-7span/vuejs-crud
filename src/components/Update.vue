<template>
  <Header />
  <h1>Hello User,welcome to update component</h1>
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
    <button type="button" v-on:click="updaterestaurent">Update</button>
  </form>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";
export default {
  name: "Update",
  data() {
    return {
      restaurent: {
        name: "",
        contact: "",
        address: "",
      },
    };
  },
  components: {
    Header,
  },
  methods: {
    async updaterestaurent() {
      const result = await axios.put(
        "http://localhost:3000/restaurents/" + this.$route.params.id,
        {
          name: this.restaurent.name,
          contact: this.restaurent.contact,
          address: this.restaurent.address,
        }
      );
      if (result.status == 200) {
        this.$router.push({ name: "Home" });
      }
    },
  },
  async mounted() {
    let user = localStorage.getItem("user-info");
    this.name = JSON.parse(user)[0].name;
    if (!user) {
      this.$router.push({ name: "Signup" });
    }
    const result = await axios.get(
      "http://localhost:3000/restaurents/" + this.$route.params.id
    );
    this.restaurent = result.data;
  },
};
</script>

<style>
</style>