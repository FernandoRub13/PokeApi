
<template>
    <div class="container">
        <h1>PokeApi</h1>
        
    </div>
    <div class="container">
        <Card :pokemon="pokemon" v-for="pokemon in pokemons"/>
    </div>
</template>

<script >

    import { defineComponent } from 'vue';
    import axios from 'axios';
    import Card from './Card.vue';

    export default defineComponent({
        components: {
            Card
        },
        data() {
            return {
                pokemons: []
            }
        },
        mounted() {
            axios.get('https://pokeapi.co/api/v2/pokemon/')
                .then(response => {
                    this.pokemons = response.data.results;

                })
        }
    });
</script>

<style>
    .container {
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        flex-wrap: wrap;
        justify-content: center;
    }
</style>