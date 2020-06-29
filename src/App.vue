<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" width="40px">
    <HelloWorld msg="Image Search based on VUE.js and unsplash API"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
body {
 background-image: url(./assets/crystal.png); 
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
</style>
