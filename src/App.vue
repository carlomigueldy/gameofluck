<template>
  <div>
    <div class="my-logo">
      <img alt="Vue logo" src="./assets/logo.png">
    </div>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import 'bootstrap' 
import 'bootstrap/dist/css/bootstrap.min.css'

export default {
  name: 'app',
  components: {
    HelloWorld
  }
}
</script>

<style>
.my-logo {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
