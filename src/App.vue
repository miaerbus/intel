<template>
  <div id="app">
    <Portal/>
  </div>
</template>

<script>
import Portal from './components/Portal.vue'

export default {
  name: 'app',
  components: {
    Portal
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
