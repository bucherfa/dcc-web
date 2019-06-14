<template>
  <div id="app">
    <div class="header">
      <span class="title">docker-compose Converter</span>
    </div>
    <Converter msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import Converter from './components/Converter.vue'

export default {
  name: 'app',
  components: {
    Converter
  }
}
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.header {
  background: #099cec;
  color: #ffffff;
  font-weight: bolder;
  width: 100%;
}

.title {
  display: inline-block;
  margin: 0.7rem;
}
</style>
