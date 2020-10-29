<template>
  <div>
    <h1>PokeGuía</h1>
    <p>Ingresa nombre de tu pokemon favorito (si no te lo sabes coloca un numero)</p>
    <form @submit.prevent="agregarPokemon">
      <label for="tarea">Nombre: </label>
      <input type="text" v-model="nombre">
      <button type="submit">Buscar</button>
    </form>
    <div class="card" style="width: 18rem;">
      <img :src="imagen" class="card-img-top" :alt="this.nombre">
      <div class="card-body">
        <h1 class="card-title">{{nombre}}</h1>
      </div>
      <ul class="list-group list-group-flush">
        <h5>Movimientos</h5>
        <li class="list-group-item" v-for="(item) in movimientos" :key="item">{{item.move.name}}</li>
      </ul>
      <ul class="list-group list-group-flush">
        <h5>Habilidades</h5>
        <li class="list-group-item" v-for="(item) in habilidades" :key="item">{{item.ability.name}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'PokeGuia',
  data() {
    return {
      nombre: '',
      imagen: '',
      movimientos: '',
      habilidades: ''

    }
  },
  methods: {
    agregarPokemon() {
      axios.get(`https://pokeapi.co/api/v2/pokemon/${this.nombre}`)
      .then((result) => {
        console.log(result.data)
        this.nombre = result.data.name;
        this.imagen = result.data.sprites.front_default;
        this.movimientos = result.data.move;
        this.habilidades = result.data.abilities;
      })
      this.nombre = '';
    }
  },
  created() {
    axios.get(`https://pokeapi.co/api/v2/pokemon/pikachu`)
    .then((result) => {
      this.nombre = result.data.name;
      this.imagen = result.data.sprites.front_default;
      this.movimientos = result.data.moves;
      this.habilidades = result.data.abilities;
    })
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
