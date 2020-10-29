<template>
  <div id="app">
    <img alt="logo" src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/International_Pok%C3%A9mon_logo.svg/1200px-International_Pok%C3%A9mon_logo.svg.png">
    <PokeGuia />
  </div>
</template>

<script>
import PokeGuia from './components/PokeGuia.vue'


export default {
  name: 'App',
  components: {
    PokeGuia,
  }
}
</script>

<style>

</style>
