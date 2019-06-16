<template>
  <div id="app">
    <div class="header">
      <span class="title">docker-compose Converter</span>
      <a class="link" href="https://github.com/bucherfa/dcc-web">
        <img class="logo" src="./assets/github.png">
      </a>
    </div>
    <Converter msg="Welcome to Your Vue.js App"/>
    <div class="footer">
      <span>Give feedback/submit an issue for </span>
      <a href="https://github.com/bucherfa/docker-compose-converter/issues">Conversion</a>
      <span> and </span>
      <a href="https://github.com/bucherfa/dcc-web/issues">UI</a>
      <span>. Using </span>
      <a href="https://www.npmjs.com/package/docker-compose-converter">docker-compose-converter</a>
      <span> version </span>
      <a :href="'https://www.npmjs.com/package/docker-compose-converter/v/' + dccVersion">{{ dccVersion }}</a>
      <span>.</span>
    </div>
  </div>
</template>

<script>
import Converter from './components/Converter.vue'
import packageJSON from '../package.json'

export default {
  name: 'app',
  components: {
    Converter
  },
  computed: {
    dccVersion () {
      return packageJSON.dependencies['docker-compose-converter'].split('^')[1]
    }
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
  display: flex;
  font-weight: bolder;
  justify-content: space-between;
  width: 100%;
}

.title {
  display: inline-block;
  margin: 0.7rem;
}

.logo {
  height: 2.2rem;
  margin: 0.3rem 0.7rem 0;
}

.footer {
  font-size: 0.8rem;
  padding: 0.5rem;
  text-align: center;
}
</style>
