<template>
  <div id="app">
    <AppStage/>
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
@import url('https://fonts.googleapis.com/css2?family=Comforter+Brush&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Permanent+Marker&display=swap');

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

button {
  text-transform: uppercase;
  border: 1px solid grey;
  border-radius: 10px;
  padding: 0.5rem 1rem;
  transform: all .2s;
}

button:hover {
  background-color: black;
  color: white;
  cursor: pointer;
}
</style>
