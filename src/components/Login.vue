<template>
  <img src="../assets/logo.png" class="logo" />
  <h1>welcome to login page</h1>
  <div class="login">
    <input type="text" v-model="email" placeholder="Enter your email" />
    <input
      type="password"
      v-model="password"
      placeholder="Enter your password"
    />
    <button v-on:click="login">Login</button>
    <p><router-link to="/signup">Signup up</router-link></p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Login",
  data() {
    return {
      email: " ",
      password: " ",
    };
  },
  methods: {
    async login() {
      console.warn(this.email, this.password);
      let result = await axios.get(
        `http://localhost:3000/users?email=${this.email}&password=${this.password}`
      );
      if (result.status == 200 && result.data.length > 0) {
        localStorage.setItem("user-info", JSON.stringify(result.data));
        this.$router.push({ name: "Home" });
      }
      console.warn(result);
    }
  },
  mounted() 
  {
      let user = localStorage.getItem("user-info");
      if (user) {
        this.$router.push({ name: 'Home' })      
      }
  }
};
</script>

<style>
</style>