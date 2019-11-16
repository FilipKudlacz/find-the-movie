<template>
  <div id="app" :class="[{ start: step === 1 }, 'wrapper']">
        <Header v-if="step === 0" />
        <transition name="logoSlide">
            <p class="logo" v-if="step === 1">Find the Movie</p>
        </transition>
        <InputComponent v-model="inputFilmName" @input="handleInput" :class="{ inputStepOne: step === 1}"/>
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
            loading: false,
            step: 0,
        };
    },
    methods: {
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

</style>
