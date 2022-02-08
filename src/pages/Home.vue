<template>

    <div class="select-your-pokemon">

        <img
        src="./../assets/logo-pixel.gif"
        alt="pokémon"
        >

        <div class="select-your-pokemon-content">

            <PokemonList 
            :pokemon-list="statePokemonDataList"
            :favorites="stateFavoritePokemonList"
            @deleteFavorite="deleteFavorite"
            @addFavorite="addFavorite"
            />

            <SummaryFavorites
            :pokemon-list="statePokemonDataList"
            :favorites="stateFavoritePokemonList"
            @addFavorite="addFavorite"
            @eraseFavoritePokemonList="eraseFavoritePokemonList"
            />

        </div>

    </div>
    
</template>

<script>

const axios = require('axios').default;
import { mapState, mapActions } from 'vuex';
import PokemonList from '../components/PokemonList.vue'
import SummaryFavorites from '../components/SummaryFavorites.vue'



export default {
    name: 'Home',
    components: {
        PokemonList,
        SummaryFavorites
    },
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
            const json = await response.data;
            return json.results;
            
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