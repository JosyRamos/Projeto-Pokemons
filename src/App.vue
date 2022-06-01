<template>
<v-app>
  <v-container>
    <v-card>
      <v-container>
        <v-text-field 
        v-model="search"
        label="Pesquisar"
        placeholder="Chamander"
        solo>
        </v-text-field>
  
        <v-row>
          <v-col cols="2" v-for="pokemon in filtered_pokemons " :key="pokemon.name">
            <v-card>
              <v-container>
              <v-row class="mx-0 d-flex justify-center">
              {{get_id(pokemon)}}
          <img :src= " `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${get_id(pokemon)}.png `"
              
              :alt="pokemon.name"
              width=100%/>
              </v-row>
              <h2 class = "text-center">{{get_name(pokemon)}}</h2>
              </v-container>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-card>
  </v-container>
</v-app>
</template>

<script>
import axios from 'axios';
export default {
  name: 'App',

  components: {

  },

  data() {
    return {
      pokemons: [],
      search:"",
    }

  },
  computed:{
    filtered_pokemons(){
      return this.pokemons.filter((item)=>{
        return item.name.includes(this.search);
      })

    }
  },
  methods:{
    get_id(pokemon){
      return Number(pokemon.url.split("/")[6])
    },
    get_name(pokemon){
      return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1);

    }
  },
  mounted() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151").then((response) => {
      this.pokemons = response.data.results;
    })
  }

};
</script>

<style>
#app {
  backgroud: linear-gradient(to bottom right, rgba(10, 10, 10, 1),
      rgba(12, 39, 63, 1),
    ) no-repeat center center fixed !important;
  -webkit-backgroud-size: cover;
  -o-backgroud: cover !important;
  backgroud-position: center;
  main-heigth: 100vh;

}
</style>
