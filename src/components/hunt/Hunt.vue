
<template>
    <section>
        <div class="hunt">
            <button v-show="showHunt" @click="seCurrenttPokemon">Procurar</button>
            <pokemon v-show="showPokemon" :pokemon="currentPokemon" />
            <button v-show="showPokemon" @click="capture">Capturar</button>
        </div>
        <pokemon-list v-show="showCaptured" :pokemonsList="capturedList"></pokemon-list>
    </section>
</template>

<script>

import Pokemon from './../pokemon/Pokemon.vue'
import PokemonList from './../pokemon-list/PokemonList.vue'

export default {

    data() {
        return {
            pokemonList: [],
            capturedList: [],
            currentPokemon: {},
            showPokemon: false,
            showHunt: false,
            showCaptured: false
        }
    },
    
    components: {
        pokemon: Pokemon,
        'pokemon-list': PokemonList
    },

    created() {
        this.$http.get('https://pokeapi.co/api/v2/pokemon').then(resp => resp.json()).then(info => {
            return this.$http.get('https://pokeapi.co/api/v2/pokemon/?offset=0&limit='+info.count).then(resp => resp.json()).then(pokemons => {
                this.pokemonsList = this.setPokemonIdAndCount(pokemons.results)
                this.showHunt = true
            })
        })
    },

    methods: {
        
        setPokemonIdAndCount (pokemonsList) {
            return pokemonsList.map(pokemon => {
                const aux = pokemon.url.split('/')
                return { ...pokemon, id: aux[aux.length - 2], count: 0 }
            })
        },

        seCurrenttPokemon () {
            const number = Math.floor(Math.random()*this.pokemonsList.length) + 1;
            this.currentPokemon = this.pokemonsList[number]
            this.showPokemon = true
        },

        capture () {
            const index = this.capturedList.indexOf( this.currentPokemon )
            if (index >= 0) {
                this.capturedList[index]['count'] = this.capturedList[index]['count'] ? this.capturedList[index]['count'] + 1 : 2
            } else {
                this.capturedList.unshift( this.currentPokemon )
                this.showCaptured = true
            }
        }

    }

}

</script>

<style scoped lang="scss">

    .hunt {
        display: flex;
        max-width: 500px;
        justify-content: space-evenly;
        align-items: center;
        margin: 24px auto;
        background-image: url('./../../assets/images/grass.png');
        background-position: center top;
        background-repeat: no-repeat;
        background-size: cover;
    }

</style>
