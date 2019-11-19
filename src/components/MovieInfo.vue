<template>
    <div class="movieInfoWrapper">
        <img :src="`http://image.tmdb.org/t/p/w154//${movieData.poster_path}`" alt="Movie Poster">
        <div class="textInfo">
            <p class="title"> {{movieData.title}} </p>
            <p> Popularity: {{movieData.popularity}} </p>
            <p> {{movieData.vote_count}} votes</p>
        </div>
    </div>
</template>

<script>
export default {
    name: "MovieInfo",
    props: {
        movieData: {
            type: Object,
            required: true,
        },
    },
}
</script>

<style lang="scss" scoped>
.movieInfoWrapper {
    width: auto;
    display: grid;
    grid-template-columns: auto auto;
    margin: 10px 0;
    align-items: center;
    
    @media screen and (min-width: 1024px) {
        margin: 10px 30px;
    }

    &:hover {
        background-color: #3e5771;
    }
}

img {
    margin-right: 10px;

    @media screen and (max-width: 765px) {
        width: 120px;
        height: auto;
        margin-right: 5px;
    }
}

.movieInfoWrapper:hover {
    cursor: pointer;
}

.textInfo {
    justify-content: center;
    margin: 35px 0;

    @media screen and (min-width: 1024px) {
        width: 200px;
    }
}

.title {
    font-weight: bold;
    color: #ff8300;
}
</style>