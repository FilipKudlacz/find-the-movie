<template>
    <div class="wrapper">
        <Header />   
        <InputComponent v-model="inputFilmName" @input="handleInput"/>
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
import Header from '@/components/Header.vue'
import InputComponent from '@/components/InputComponent.vue'
import debounce from 'lodash.debounce'

const API = 'https://api.themoviedb.org/3';

export default {
    name: "MainPage",
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
        handleInput: debounce( function() {
            axios.get(`${API}/search/movie?api_key=${apiKey}&query=${this.inputFilmName}`)
            .then((response) => {
                // eslint-disable-next-line no-console
                console.log(response);
                this.movies = response.data.results;
            });
        }, 700),
    },
}
</script>

<style scoped>
.wrapper {
    margin-top: 130px;
}

p {
    font-size: 16px;
}

input:focus {
    outline: none;
}

ul {
    list-style-type: none;
    padding: 0px;
}
</style>