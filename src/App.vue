<template>
  <div id="app" class="wrapper">
      <Header />   
      <InputComponent v-model="inputFilmName" @input="handleInput"/>
      <hr>  
      <ul >
        <li v-for="item in movies" :key="item.id">
            <p class="result">{{ item.title }}</p>
        </li>
      </ul>
  </div>
</template>

<script>
import axios from 'axios';
import { apiKey } from './../key.json';
import Header from '@/components/Header.vue'
import InputComponent from '@/components/InputComponent.vue'
import debounce from 'lodash.debounce'

const API = 'https://api.themoviedb.org/3';

export default {
    name: "app",
    components: {
        Header,
        InputComponent,
    },
    data() {
        return {
            inputFilmName: '',
            movies: [],
        };
    },
    methods: {
        handleInput: debounce(function() {
            // eslint-disable-next-line no-console
            console.log('hello1');
            axios.get(`${API}/search/movie?api_key=${apiKey}&query=${this.inputFilmName}`)
            .then((response) => {
                // eslint-disable-next-line no-console
                console.log(response);
                this.movies = response.data.results;
            })
            .catch((error) => {
                // eslint-disable-next-line no-console
                console.log(error);
            });
        }, 700),
    },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  box-sizing: border-box;
}

body {
  background-color: #2c3e50;
}

.wrapper {
    padding: 30px;
    margin: 0;
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.result {
    font-size: 16px;
}

ul {
    list-style-type: none;
    padding: 0px;
}

hr {
  width: 70%;
}

</style>
