<template>
  <div id="app">
   <div class="column is-half is-offset-one-quarter">
    <img src="./assets/abiezer.png" alt="Logo Abiezer" class="bi">
    <hr />
    <h1 class="is-size-2">POKEDEX - BIBI</h1>
    <input class="input is-rounded" type="text" placeholder="Buscar Pokedex" v-model="busca">
    <button class="button is-fullwidth is-success" id="btnBuscar" @click="buscar">Buscar</button>
    <div v-for="(poke,index) in filteredPokemons " :key="poke.url">
      <PokemonBi :num="index+1" :name="poke.name" :url="poke.url" />
    </div>
   </div>
  </div>
</template>

<script>
import axios from "axios"
import PokemonBi from "./components/PokemonBi";

export default {
  name: 'App',
  data(){
    return{
      pokemons:[],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res =>{
      console.log("Pegou os pekoemons")
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    })
  },
  components: {
    PokemonBi
  },
  methods: {
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ''){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(poke => poke.name == this.busca);
      }
    }
  }

  /*computed: {
    resultadoBusca: function(){
      if(this.busca == '' || this.busca == ''){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name ==  this.busca)
      }
    }
  }*/
  
}
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
#btnBuscar {
  margin-top: 2%;
}
</style>
