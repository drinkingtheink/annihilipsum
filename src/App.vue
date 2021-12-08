<template>
  <div id="app">
    <Background class="background" />
    <AppStage/>
  </div>
</template>

<script>
import AppStage from './components/AppStage.vue'
import Background from './components/Background.vue'

export default {
  name: 'App',
  components: {
    AppStage,
    Background
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Smooch&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Comforter+Brush&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Permanent+Marker&display=swap');

/** FROM: https://coolors.co/001219-005f73-0a9396-94d2bd-e9d8a6-ee9b00-ca6702-bb3e03-ae2012-9b2226 */
/** blue1 */
/* #001219 */
/** blue2 */
/* #005F73 */
/** bluegreen1 */
/* #0A9396 */
/** bluegreen2 */
/* #94D2BD */
/** yellow1 */
/* #E9D8A6 */
/** yellow2 */
/* #EE9B00 */
/** orange1 */
/* #CA6702 */
/** orange 2 */
/* #BB3E03 */
/** orange 3 */
/* #AE2012 */
/** red1 */
/* #9B2226 */

html, body {
  background-color: #001219 !important;
  position: relative;
}

body {
  margin: 0;
  padding: 0;
}

h1 {
  color: #94D2BD;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 1400px;
  margin: 0 auto;
  position: relative;
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

.background {
  position: absolute;
  width: 100%;
  left: 0;
  right: 0;
  margin: auto;
}
</style>
