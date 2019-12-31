<template>
  <div id="app">
    <img alt="F1" src="./assets/iconF1.png">
    <F1Screen msg="Bem vindo ao F1 App Vue"/>
  </div>
</template>

<script>
import F1Screen from './components/F1Screen.vue'

export default {
  name: 'app',
  components: {
    F1Screen
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #333;
  margin-top: 60px;
}
</style>
