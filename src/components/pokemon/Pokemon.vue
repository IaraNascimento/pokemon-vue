
<template>
    <div class="pokemon-wrap" v-show="showInfo">
        <p class="pokemon-name">{{ pokemon.name }}</p>
        <img class="pokemon-img" :src="showInfo? pokemonInfo.sprites.front_default : null" />
    </div>
</template>

<script>

export default {

    props: ['pokemon'],

    data() {
        return {
            pokemonInfo: undefined,
            showInfo: false
        }
    },

    created() {
        this.getPokemonInfo()
    },

    watch: {
        'pokemon': function (newListValue) {
            this.getPokemonInfo()
        }
    },

    methods: {
        
        getPokemonInfo () {
            if (this.pokemon['id']) {
                this.$http.get('https://pokeapi.co/api/v2/pokemon/'+this.pokemon.id).then(resp => resp.json()).then(pokemonInfo => {
                    this.pokemonInfo = pokemonInfo
                    this.showInfo = true
                })
            }
        }

    }


}

</script>

<style scoped lang="scss">

    .pokemon {
        &-wrap {
            text-align: center;
        }
        &-name {
            width: 100%;
            max-width: 120px;
        }
        &-img {
            max-width: 96px;
            max-height: 96px;
        } 
    }

</style>
