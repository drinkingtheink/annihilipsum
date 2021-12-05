<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <AppStage msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import AppStage from './components/AppStage.vue'

export default {
  name: 'App',
  components: {
    AppStage
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Smooch&display=swap');

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
