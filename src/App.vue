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
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');

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
  border-top: 5px solid #94D2BD;
}

body {
  margin: 0;
  padding: 0;
}

h1 {
  color: #94D2BD;
  margin: 0;
  padding-top: 1.5rem;
  font-size: 3rem;
}

h1, h2, h3, h4, h5 {
  font-family: 'Bebas Neue', cursive;
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
  padding: 0.5rem 2rem;
  transition: all .2s;
  font-family: 'Bebas Neue', cursive;
  font-size: 1.5rem;
  background-color: #001219;
  border-color: #001219;
  color: #EE9B00;
}

button:hover {
  background-color: #EE9B00;
  color: red;
  cursor: pointer;
}

button.active {
  color: white;
}

.background {
  position: absolute;
  width: 100%;
  left: -2rem;
  right: 0;
  margin: auto;
}
</style>
