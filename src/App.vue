<script setup lang="ts">
    import { ref } from 'vue';
    import CardComponent from './components/CardComponent.vue';
    import type Pelicula from './interface/Pelicula.ts';
    import movies from './resource/movies.ts';
    //Crear un array boolean para el "Me gusta" o "No me gusta", indexado por el id de la pelicula
    const opinionMovie=ref<boolean[]>([])
        movies.forEach(
            movie => { opinionMovie.value[movie.id] = false;} //para que aparezca el boton "Me gusta"
        );
    //Funcion para el evento clic en el boton "Me Gusta" o "No me gusta"
    function HizoClic(UnaPelicula: Pelicula) {
        //Cambiar de estado
        opinionMovie.value[UnaPelicula.id] = !opinionMovie.value[UnaPelicula.id];
        //Incrementar o Decrementar los likes segun el estado
        if(opinionMovie.value[UnaPelicula.id]){
            UnaPelicula.likes++
        }else
            UnaPelicula.likes--
    }
</script>

<template>
    <h1>Listado de Películas</h1>
    <article class="pelicula" v-for="UnaPelicula in movies">
        <CardComponent :Peli="UnaPelicula" :gusta="opinionMovie[UnaPelicula.id]" @update_likes="HizoClic"/>
    </article>
</template>

<style scoped>
    .h1 {
        font-size: 3em;
        font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    }
    .pelicula {
        display: inline-block;
        width: fit-content;
        padding: 0.5em;
    }
</style>
