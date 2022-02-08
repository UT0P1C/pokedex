<template>
    <div>
        <h1 class="overview-favorite-pokemon__title">
        Your favorite Pokémon
        </h1>
        <div class="overview-favorite-pokemon">
        <PokemonCard
            v-for="(pokemon, index) in stateFavoritePokemonList"
            :key="index"
            :pokemon-name="pokemon"
        />
        <router-link
        class="nes-btn"
        to="/"
        >
        Go back
        </router-link>
        </div>
    </div>
</template>

<script>
import { mapState } from 'vuex'
import PokemonCard from '@/components/PokemonCard'
    export default {
        components: {
            PokemonCard
        },
        computed: {
            ...mapState([
            'stateFavoritePokemonList'
            ])
        }
    }
</script>

<style scoped>
.overview-favorite-pokemon {
    display: grid;
    grid-template-columns: 1fr 1fr;
}
.overview-favorite-pokemon__title {
    
    margin-top: 10px;
    text-align: center;
    text-shadow: 0.1em 0.1em 0.2em black;

}


</style>