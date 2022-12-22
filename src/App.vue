<template>
  <div id="app">
    <Juego/>
  </div>
</template>

<script>
import Juego from './componentes/juego.vue'

export default {
  name: 'App',
  components: {
    Juego
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #6b6b6b;
  margin-top: 60px;
}
</style>
