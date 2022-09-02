<template>
  <img src="../assets/logo.png" class="logo" />
  <h1>welcome to sign up page</h1>
  <div class="register">
    <input type="text" v-model="name" placeholder="Enter your name" />
    <input type="email" v-model="email" placeholder="Enter your email" />
    <input type="text" v-model="password" placeholder="Enter your password" />
    <button v-on:click="signUp">Signup</button>
    <p>
    <router-link to="/login" >Login</router-link>
    </p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Signup",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods:{
    async signUp() 
    {
      //  console.warn(this.name,this.email,this.password);
      let result = await axios.post("http://localhost:3000/users", {
        name: this.name,
        email: this.email,
        password: this.password,
      });
      //console.warn(result);
      if (result.status == 201) 
      {
        //alert("Signup successful");
        localStorage.setItem("user-info", JSON.stringify(result.data));
        this.$router.push({ name: "Home" });
      }
    }       
  },
  mounted() 
  {
      let user = localStorage.getItem("user-info");
      if (user) {
        this.$router.push({ name: 'Home' })      
      }
  }
}
</script>

<style>

</style>