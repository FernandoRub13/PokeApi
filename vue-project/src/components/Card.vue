<template>
    <div class="card">
        <h3 class="text-center">{{ name }}</h3>
        <div class="centered">
            <img :src="image" alt="">
        </div>
        <div class="separator"></div>
        <div class="text-center container line-h">
            <div class="left-square" >
                <p>Height: {{ height }}</p>
                <p>Weight: {{ weight }}</p>
            </div>
            <div  >
                <p>Abilities:</p>
                <ul class="list">
                    <li v-for="ability in abilities">{{ ability.ability.name }}</li>
                </ul>
            </div>                    
        </div>
        <div class="separator"></div>
        <div class="text-center container line-h">
            <div class="left-square" >
                <p>Types:</p>
                <ul class="list">
                    <li v-for="type in types">{{ type.type.name }}</li>
                </ul>
            </div>
            <div  >
                <p>Moves:</p>
                <ul class="list">
                    <li v-for="move in firstThreeMoves">{{ move.move.name }}</li>
                </ul>
            </div>
        </div>
        <div class="separator"></div>
        <div class="text-center container line-h">
            <div  >
                <p>Stats:</p>
                <ul class="list">
                    <li v-for="stat in stats">{{ stat.stat.name }}: {{ stat.base_stat }}</li>
                </ul>
            </div>
        </div>

    </div>
</template>

<script >

    import { defineComponent } from 'vue';
    import axios from 'axios';

    export default defineComponent({
        data() {
            return {
                image: '',
                abilities: [],
                height: "",
                weight: "",

                firstThreeMoves: [],
                stats: [],
                types: [],
            }
        },
        props: {
            pokemon: {
                type: Object,
                required: true
            }
        },
        mounted() {
            axios.get(this.pokemon.url)
                .then(response => {
                    console.log(response.data);
                    this.image = response.data.sprites.front_default;
                    this.height = response.data.height;
                    this.weight = response.data.weight;
                    this.abilities = response.data.abilities;
                    this.firstThreeMoves = response.data.moves.slice(0, 3);
                    this.stats = response.data.stats;
                    this.types = response.data.types;
                })
        },
        computed: {
            name() {
                // to upper case
                return this.pokemon.name.toUpperCase();
            },
        }

    });
</script>

<style>
    .card {
        width: 200px;
        height: auto;
        background-color: #f5f5f5;
        margin: 10px;
        padding: 10px;
        border-radius: 10px;
        border: 1px solid #ccc;
    }
    .text-center {
        text-align: center;
    }
    .centered {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .separator {
        width: 100%;
        height: 1px;
        background-color: #ccc;
        margin: 10px 0;
    }
        .container {
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        flex-wrap: wrap;
        justify-content: center;
    }

    .list {
        font-size: 0.8em;
    }
    .line-h {
        line-height: 0.8em;
    }
    .left-square {
        border-right: 1px solid #ccc;
        padding-right: 10px;
    }   
</style>
