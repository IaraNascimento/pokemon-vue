
<template>
    <ul class="pokemon-list">
        <li v-for="pokemon of pokemonsList">
            <span v-show="pokemon.count > 1" class="pokemon-count">{{ pokemon.count }}</span>
            <pokemon :pokemon="pokemon" />
        </li>
    </ul>
</template>

<script>

import Pokemon from './../pokemon/Pokemon.vue'

export default {

    props: ['pokemonsList'],

    components: {
        pokemon: Pokemon
    }

}

</script>

<style scoped lang="scss">

    .pokemon {
        &-list {
            margin: 24px;
            display: flex;
            flex-wrap: wrap;
            justify-content: space-evenly;
            li {
                position: relative;
                display: inline-block;
                padding: 8px;
                width: 120px;
                height: 120px;
                text-align: center;
                border: 2px solid #f39c12;
                background-color: rgba(243, 156, 18, .2);
                border-radius: 4px;
                margin: 4px;
                overflow: hidden;
            }
        }
        &-count {
            position: absolute;
            top: 40px;
            right: 12px;
            background-color: #e67e22;
            color: white;
            min-width: 24px;
            height: 24px;
            border-radius: 12px;
            text-align: center;
            padding: 4px 2px 0 2px;
            box-sizing: border-box;
        }
    }

</style>
