
<template>
    <input type="search" @input="filter" :placeholder="placeholder" />
</template>

<script>

export default {
    
    props: ['list', 'placeholder'],

    methods: {
        filter (event) {
            let filtered = this.list
            if(event.target.value) {
                let exp = new RegExp(event.target.value.trim(), 'i')
                filtered = this.list.filter(pokemon => exp.test(pokemon.name + pokemon.id))
            }
            this.$emit('filtered', filtered)
        }
    }

}

</script>

<style lang="scss">

    input {
        width: calc(100% - 48px);
        margin: 24px;
        border-radius: 4px;
        padding: 8px;
        font-size: 16px;
        border: 2px solid #f39c12;
    }

</style>
