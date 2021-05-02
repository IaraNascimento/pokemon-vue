
<template>
    <div>
        <search :list="pokemonsList" :placeholder="'Buscar por nome ou id...'" @filtered="filteredList" />
        <pokemon-list :pokemonsList="pokemonsListFiltraded"></pokemon-list>
    </div>
</template>

<script>

import Search from './../search/Search.vue'
import PokemonList from './../pokemon-list/PokemonList.vue'

export default {

    data() {
        return {
            pokemonsList: [],
            pokemonsListFiltraded: []
        }
    },

    components: {
        search: Search,
        'pokemon-list': PokemonList
    },

    created() {
        this.$http.get('https://pokeapi.co/api/v2/pokemon').then(resp => resp.json()).then(info => {
            return this.$http.get('https://pokeapi.co/api/v2/pokemon/?offset=0&limit='+info.count).then(resp => resp.json()).then(pokemons =>
                this.pokemonsList = this.setPokemonId(pokemons.results)
            )
        })
    },

    watch: {
        'pokemonsList': function (newListValue) {
            this.pokemonsListFiltraded = newListValue
        }
    },

    methods: {
        
        setPokemonId (pokemonsList) {
            return pokemonsList.map(pokemon => {
                const aux = pokemon.url.split('/')
                return { ...pokemon, id: aux[aux.length - 2] }
            })
        },

        filteredList (list) {
            this.pokemonsListFiltraded = list
        }

    }

}

</script>

<style scoped lang="scss">
</style>
