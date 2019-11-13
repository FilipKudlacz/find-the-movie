<template>
    <div>
        <h1>Find-the-Movie</h1>
        <Label for="movieInput">
            <input type="text" placeholder="Movie Name" v-model="inputFilmName" name="movieInput" @keyup.enter="handleInput">
        </Label>
        <hr>  
        <ul >
            <li v-for="item in movies" :key="item.id">
                <p>{{ item.title }}</p>
            </li>
        </ul>
    </div>
</template>

<script>
import axios from 'axios';
import { apiKey } from './../../key.json';

const API = 'https://api.themoviedb.org/3';

export default {
    name: "MainPage",
    components: {
    },
    data() {
        return {
            inputFilmName: '',
            movies: [],
        };
    },
    methods: {
        handleInput() {
            axios.get(`${API}/search/movie?api_key=${apiKey}&query=${this.inputFilmName}`)
            .then((response) => {
                // eslint-disable-next-line no-console
                console.log(response);
                this.movies = response.data.results;
            });
        },
    },
}
</script>

<style scoped>
input {
  height: 30px;
  width: 300px;
  font-size: 20px;
  text-align: center;
  border: 0;
  border-bottom: 2px solid #ff8300;
  background-color: #2c3e50;
  margin-bottom: 20px;
  color: white;
}
</style>