<template>
  <div class="container-fluid mt-3">
    <div class="jumbotron">
      <h5>NT2 - TP4 - Lucas Krigun</h5>
      <h1>Bienvenidos a VueJS CLI</h1>
      <br>
      <Navbar/>
      <router-view></router-view>
  </div>
  </div>
</template>




<script>

import Navbar from './components/Navbar.vue'


export default {
  name: 'App',
  components: {
    Navbar,

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
