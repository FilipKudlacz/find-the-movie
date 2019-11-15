<template>
    <div class="headerWrapper" >
        <h1 class="name">
            Find the Movie
        </h1>
        <p class="description">
            Welcome to your movie finder! You give us a phrase, and we find movies with your phrase in their title!
        </p>
        <p class="instruction">
            Input your phrase below
        </p> 
    </div>
</template>

<script>
export default {
    name: "Header"
}
</script>

<style scoped>

.headerWrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    width: 100%;
}

.name {
  font-size: 52px;
  font-family: monospace;
}

.description {
    font-size: 22px;

    max-width: 450px;
}

.instruction {
    font-size: 15px;
    margin-bottom: 20px;
}


</style>