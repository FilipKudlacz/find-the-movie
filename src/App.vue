<template>
  <div id="app" :class="[{ start: step === 1 }, 'wrapper']">
        <Header v-if="step === 0" />
        <transition name="logoSlide">
            <p class="logo" v-if="step === 1">Find the Movie</p>
        </transition>
        <InputComponent v-model="inputFilmName" @input="handleInput" :class="{ inputStepOne: step === 1}"/>
        <hr>  
        <div class="movieList" v-if="step === 1">
            <MovieInfo v-for="movie in movies" :key="movie.id" :movieData="movie" @click.native="openDescription(movie)" />
        </div>
        <MovieDetails v-if="descriptionOpen" :movieDetails="descriptionData" @closeDetails="descriptionOpen = false"/>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce'
import { apiKey } from './../key.json';
import Header from '@/components/Header.vue'
import InputComponent from '@/components/InputComponent.vue'
import MovieInfo from '@/components/MovieInfo.vue'
import MovieDetails from '@/components/MovieDetails.vue'

const API = 'https://api.themoviedb.org/3';

export default {
    name: "app",
    components: {
        Header,
        InputComponent,
        MovieInfo,
        MovieDetails,
    },
    data() {
        return {
            inputFilmName: '',
            movies: [],
            loading: false,
            step: 0,
            descriptionOpen: false,
            descriptionData: null,
        }
    },
    methods: {
        openDescription(object) {
            this.descriptionOpen = true;
            this.descriptionData = object;
        }, 

        handleInput: debounce(function() {
            this.loading = true;
            axios.get(`${API}/search/movie?api_key=${apiKey}&query=${this.inputFilmName}`)
            .then((response) => {
                // eslint-disable-next-line no-console
                console.log(response);
                this.movies = response.data.results;
                this.loading = false;
                this.step = 1;
            })
            .catch((error) => {
                // eslint-disable-next-line no-console
                console.log(error);
            });
        }, 600),
    },
};
</script>

<style lang="scss">
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

    &.start {
        margin-top: 20px;
    }
}

.inputStepOne {
    margin-top : 80px;
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

.logo {
    position: absolute;
    top: 45px;
    font-family: monospace;
    font-size: 25px;
    font-weight: bold;
}

.logoSlide-enter-active, .logoSlide-leave-active {
    transition: margin-top 0.2s ease;
}

.logoSlide-enter, .logoSlide-leave {
    margin-top: -50px;
}

.movieList {
    display: grid;
    grid-template-columns: auto;
    margin: 20px 0;

    @media screen and (min-width: 1024px) {
        grid-template-columns: auto auto;
    }
}

</style>
