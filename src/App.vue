<template>
  <div id="app">
    <Repos :browserName="browserName" />
  </div>
</template>

<script>
/* eslint-disable */
import uaParser from 'ua-parser-js'
import Repos from './components/Repos.vue'
import 'bootstrap/dist/css/bootstrap.min.css'
export default {
  name: 'app',
  components: {
    Repos
  },
  data() {
    return {
      browserName: ''
    }
  },
  created() {
    const parser = new uaParser()
    this.browserName = parser.getResult().browser.name
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
