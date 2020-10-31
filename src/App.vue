<template>
  <div>
    <img alt="logo" src="../src/assets/20088202213.jpg">
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
img {
  width: 100%;

}
</style>
