<template>
  <div>
    <h1 class="text-center">PokeGuía</h1>
    <p class="text-center">Ingresa nombre de tu pokemon favorito (si no te lo sabes coloca un numero)</p>

    <form class="container text-center" @submit.prevent="agregarPokemon(nombre)">
      <div class="form-group">
        <label for="tarea">Nombre: </label>
        <input type="text" class="form-control" v-model="nombre">
      </div>
      <button type="submit" class="btn btn-info">Buscar</button>
    </form>


    <h1 class="text-center nombrePoke">{{nombre}}</h1>
    <section class="row carta">
      <div class="card text-center col-12" style="width: 18rem;">
        <div class="card-header">
          <img :src="imagen" class="imagePoke" :alt="this.nombre" >
        </div>
        <ul class="list-group list-group-flush">
          <h5>Movimientos</h5>
          <li class="list" v-for="(item, index) in movimientos" :key="index">{{item.move.name}}</li>
        </ul>
        <ul class="list-group list-group-flush">
          <h5>Habilidades</h5>
          <li class="list" v-for="(item, index) in habilidades" :key="index">{{item.ability.name}}</li>
        </ul>
      </div>
    </section>
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
      habilidades: [],
      movimientos: [],

    }
  },
  methods: {
    agregarPokemon(pokemon) {
      if(pokemon)
        axios.get(`https://pokeapi.co/api/v2/pokemon/${pokemon}`)
        .then(json => {
          console.log(json.data)
          this.nombre = json.data.name;
          this.imagen = json.data.sprites.front_default;
          this.movimientos = json.data.moves;
          this.habilidades = json.data.abilities;
        })
        .catch(error => console.log(error))
    }
  },
  created() {
    this.nombre = 'pikachu';
    this.agregarPokemon('pikachu');
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.form-control {
  display: inline-block;
  width: 25%;
  margin-left: 10px;
}

.carta {
  padding: 0 6.5rem 0 6.5rem;
}

.list {
  list-style: none;
}

.imagePoke {
  width: 120px;
}

.nombrePoke {
  font-size: 60px;
  text-transform: capitalize;
  color: darkgoldenrod;
}
</style>
