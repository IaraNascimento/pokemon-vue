
<template>
  <main>
    <pokemon-menu :routes="routes" />
    <router-view></router-view>
  </main>
</template>

<script>

import Menu from './components/menu/Menu.vue'
import { routes } from './routes'

export default {

  data() {
    return {
      routes,
      pokemonsList: []
    }
  },

  components: {
    'pokemon-menu': Menu,
  },

}

</script>

<style lang="scss">

  @import './assets/styles/reset';
  @import './assets/styles/buttons';

  html, body {
    font-family: Arial, sans-serif;
  }

  html {
    overflow-y: scroll;
  }

</style>
