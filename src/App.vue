<template>
  <div id="app">
    <main-page></main-page>
  </div>
</template>

<script>
import MainPage from './views/MainPage.vue'

export default {
  name: 'app',
  components: {
    MainPage
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
  box-sizing: border-box;
}

body {
  background-color: #2c3e50;
}

h1 {
  font-size: 52px;
  font-family: monospace;
}

hr {
  width: 70%;
}
</style>
