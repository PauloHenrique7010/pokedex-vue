<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/logo.png" />
      <hr>
      <h4 class="is-size-4">Pokedex</h4>
      <input type="text" class="input is-rounded" v-model="busca" placeholder="Buscar pokemon pelo nome">
      <button class="button is-fullwidth is-success" @click="buscar" id="btnBusca">Buscar</button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :num="index + 1" :url="poke.url" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";
//https://pokeapi.co/api/v2/pokemon/?limit=151&offset=0.

export default {
  name: "App",
  data() {
    return {
      busca: '',
      pokemons: [],
      filteredPokemons: [],
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon/?limit=151&offset=0.")
      .then((res) => {
        this.pokemons = res.data.results;
        this.filteredPokemons = this.pokemons;
      });
  },
  components: {
    Pokemon,
  },
  methods:{
    buscar: function(){
      console.log('aqui');
      this.filteredPokemons = this.pokemons;
      if (this.busca != ""){
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);        
      }

    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#btnBusca{
  margin-top: 2%;

}
</style>
