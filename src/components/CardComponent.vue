<script setup lang="ts">
    import type Pelicula from '../interface/Pelicula.ts';
    
    const props = defineProps<{Peli: Pelicula, gusta: boolean}>()
    const emits = defineEmits(['update_likes'])
    function likes() {
        emits('update_likes', props.Peli )
    }
</script>

<template>
    <p class="titulo">{{props.Peli.titulo}}</p>
    <p>{{props.Peli.director}}</p>
    <p>{{props.Peli.generos}}</p>
    <p>{{props.Peli.anio}}</p>
    <div v-if="props.Peli.portada"> 
        <img class="portada" :src="props.Peli.portada" :alt="`Imagen de la pelicula: ${props.Peli.titulo}`"/>
    </div>
    <div v-else> 
        <img class="portada" src="../resource/no-disponible.png" alt="Portada no disponible"/>
    </div>
    <p>Likes = {{props.Peli.likes}}</p>
    <div v-if="props.gusta">
        <button class="bot-no-me-gusta" @click="likes">No me gusta</button>
    </div>
    <div v-else="props.gusta">
        <button class="bot-me-gusta" @click="likes">Me gusta</button>
    </div>
</template>

<style scoped>
    .bot-me-gusta {
        color:black;
        background-color:forestgreen;
    }
    .bot-no-me-gusta {
        color: black;
        background-color:indianred;
    }
    p {
        font-weight: 500;
        font-size: 1.1em;
        width: 14em;
        margin: auto;
    }
    .titulo {
        font-weight: bold;
        font-size: 1.4em;
        width: 14em;
        margin: auto;
    }
    .portada {
        height: 20em;
        width: 14em;
        display: block;
        margin: 1em auto;
        border: 1px solid green;
        box-shadow: 0 0 10px rgba(0, 255, 255, 0.7),
                    0 0 20px rgba(0, 255, 128, 0.5),
                    0 0 40px rgba(247, 121, 4, 0.753);
        border-radius: 4px;
        transition: transform 0.4s ease, box-shadow 0.3s ease;
    }
    .portada:hover {
        transform: scale(1.05);
        box-shadow: 0 0 15px rgba(0, 255, 255, 0.9),
                    0 0 30px rgba(37, 13, 104, 0.7),
                    0 0 60px rgba(221, 6, 192, 0.5);
    }
    .portada.img {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }
</style>