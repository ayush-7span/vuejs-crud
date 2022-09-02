<template>
  <div class="nav">
    <router-link to="/" >Home</router-link>
    <router-link to="/add" >add restaurant</router-link>
    <!--<router-link to="/update" >update restaurant</router-link>-->
    <a v-on:click='logout'>Logout</a>
  </div>
</template>

<script>
export default {
  name: "Header",
  methods:{
      logout(){
          console.warn('logout')
          localStorage.clear();
          this.$router.push({ name: 'Login' }) 
      }
  }
};
</script>

<style>
body{
  padding: 0;
  margin: 0;
}
.nav {
  background-color: seashell;
  overflow: hidden;
}
.nav a {
  float: left;
  color: seagreen;
  padding: 14px 16px;
  text-align: center;
  text-decoration: none;
  font-size: 12px;
  margin-right: 5px;
}
</style>