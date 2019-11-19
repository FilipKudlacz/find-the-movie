<template>
    <div class="outerWrapper">
        <div class="innerWrapper">
            <div class="upperInfo">
                <img :src="`http://image.tmdb.org/t/p/w154//${movieDetails.poster_path}`" alt="Movie Poster">
                <div class="upperText">
                    <h3 class="movieTitle"> {{ title }} </h3>
                    <p v-if="this.movieGenres.length > 0">Genres: 
                        <span v-for="genre in movieGenres" :key="genre">{{genre}}</span>
                    </p>
                    <p>Popularity: {{ popularity }}</p>
                    <p>Votes: {{ votes }}</p>
                    <p>Production Country </p>
                </div>
            </div>
            <div class="textInfo">
                <a :href="linkToImdb" target="_">Go to IMDB site</a>
                <p class="description">{{description}}</p>
            </div>
            <div class="close" @click="$emit('closeDetails')">
            </div>
        </div>
    </div>
</template>

<script>
import genres from './../../genres.json'
import { apiKey } from './../../key.json'
import axios from 'axios'

export default {
    name: "MovieDetails",
    props: {
        movieDetails: {
            type: Object,
            required: true,
        },
    },
    data() {
        return {
            title: '',
            movieGenres: [],
            popularity: '',
            votes: '',
            producedIn: '',
            linkToImdb: '',
            description: '',
        }
    },
    mounted() {
        this.title = this.movieDetails.title;
        this.popularity = this.movieDetails.popularity;
        this.votes = this.movieDetails.vote_count;
        this.description = this.movieDetails.overview;
        this.movieGenres = this.movieDetails.genre_ids.map( genreId => genres.genres[genreId]);

        axios.get(
        `https://api.themoviedb.org/3/movie/${this.movieDetails.id}?api_key=${apiKey}`)
      .then(data => {
        this.linkToImdb = `https://www.imdb.com/title/${data.data.imdb_id}`;
      });
    }
}
</script>

<style lang="scss" scoped>
.outerWrapper {
    background-color: #384f66;
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;

    @media (min-width: 768px){
        top: 20%;
        left: 15%;
        width: 70%;
        height: 60%;
    }

    @media (min-width: 1080px) {
        top: 10%;
        left: 30%;
        width: 40%;
        height: 80%;
        box-shadow: 0 30px 30px black;
    }
}

.innerWrapper {
    display: flex;
    flex-direction: column;
    height: 100%;
    padding: 20px;
    justify-content: center;
    align-items: center;
}

.upperInfo {
    display: flex;
    width: 100%;
}

.upperText {
    display: flex;
    flex-direction: column;
    margin: auto;
    margin-left: 10px;
    justify-content: center;
    text-align: center;

    @media (min-width: 768px) {
        margin-left: 30px;
    }
}
.textInfo {
    display: flex;
    flex-direction: column;
    width: 100%;
    height: 100%;
    padding: 10px;
}

.movieTitle {
    color: #ff8300;
}

.close{
    position: absolute;
    right: 10px;
    top: 10px;
    width: 30px;
    height: 30px;
    cursor: pointer;

    &::before, &::after {
        position: absolute;
        content: '';
        top: 14px;
        right: 5px;
        width: 20px;
        height: 2px;
        background: black;
        display: block;
    }

    &::before {
        transform: rotate(-45deg);
    }

    &::after {
        transform : rotate(45deg);
    }
}

.description {
    margin-top: 10px;
    height: 100%;
    overflow: scroll;
    margin-bottom: 50px;
    padding: 10px;
}

img {
    margin-left: auto;
}

p {
    margin: 5px 0;
}

a {
    color: #ff8300;
}

</style>