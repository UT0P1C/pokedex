<template>

    <div class="select-your-pokemon">

        <img
        src="./../assets/logo-pixel.gif"
        alt="pokémon"
        >

        <h1>Pick your pokemon</h1>

        <div class="select-your-pokemon-content">

        </div>

    </div>
    
</template>

<script>

const axios = require('axios').default;
import { mapState, mapActions } from 'vuex';



export default {
    name: 'Home',
    computed: {
        ...mapState(['statePokemonDataList', 'stateFavoritePokemonList']),
    },
    async created(){
        const pokemonData = await this.getPokemonData();
        this.setPokemonData(pokemonData);
    },
    methods: {
        async getPokemonData(){
            let url = 'https://pokeapi.co/api/v2/pokemon?limit=151';
            const response = await axios.get(url);
            this.result = response.data;
            JSON.stringify(this.result);
            console.log(this.result);
        },
        ...mapActions(['setPokemonData', 'addFavorite', 'deleteFavorite', 'eraseFavoritePokemonList']),
    }
}
</script>

<style scoped>

.select-your-pokemon{
    text-align: center;
}

.select-your-pokemon h1{
    text-shadow: 0.1em 0.1em 0.2em black;
}

.select-your-pokemon-content {
    text-align: left;
    display: flex;
    justify-content: space-evenly;
}

</style>