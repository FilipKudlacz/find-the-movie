<template>
  <div id="app">
    <h1>Find-the-Movie</h1>
    <p>
    <input type="text" placeholder="Movie Name" v-model="inputFilmName">
    </p>
    <hr>
    <search-result/>
  </div>
</template>

<script>
import SearchResult from './components/SearchResult.vue'

export default {
  name: 'app',
  components: {
    SearchResult
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
}

body {
  background-color: #2c3e50;
}

h1 {
  border: 3px solid white;
  font-size: 52px;
}

input {
  height: 30px;
  width: 500px;
  font-size: 20px;
  text-align: center;
}

</style>
