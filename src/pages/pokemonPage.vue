<template>
  <h1 v-if="!pokemon">Espera por favor... 🤔</h1>
  <div v-else>

      <div class="title">
        ¿Quién es este pokémon?
        <div class="img">
          <img class="pokeball" src="./../assets/pb.png"  alt="">          
        </div>
      </div>

      <!-- TODO> img -->
      <pokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon"/>

      <!-- TODO> Opciones -->
      <pokemonOptions :pokemons="pokemonArr" @selection="checkAnswer"/>

      <template class="after-selection" v-if="showAnswer">
        <h1>{{ message }}</h1>
        <button @click="newGame" class="restart">
          Nuevo juego
        </button>
      </template>
  </div>
</template>

<script>
import pokemonOptions from "../components/pokemonOptions.vue";
import pokemonPicture from "../components/pokemonPicture.vue";
import getPokemonOptions from "../helpers/getPokemonOptions";

export default {
  data(){
    return{
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: ''
    }
  },
  components:{
    pokemonOptions, pokemonPicture
  },
  methods:{
    async mixPokemonArray(){
      this.pokemonArr = await getPokemonOptions();

      const rndInt = Math.floor( Math.random() * 4 )
      this.pokemon = this.pokemonArr[ rndInt ];
    },
    checkAnswer(selectedId){
      this.showPokemon = true;      
      this.showAnswer = true;
      if( selectedId === this.pokemon.id ){
        this.message = `¡Sí! es ${this.pokemon.name}. 👌`;
      }else{
        this.message = `Oops! era ${this.pokemon.name}. 😅`;
      }
    },
    async newGame(){
      this.pokemon = null;
      this.pokemonArr = [];
      this.showPokemon = false;
      this.showAnswer = false;
      this.mixPokemonArray();
    }
  },
  mounted(){
    this.mixPokemonArray();
  },
  
}
</script>

<style >
  .restart{
    padding: 10px;
    border: none;
    border-radius: 3px;
    background: none;
    font-weight: bold;
    background-color: rgb(87, 118, 202);
    cursor: pointer;
    color: white
  }

  .title{
    font-size: 30px;
    margin: auto;
    width: 90%;
    margin-bottom: 30px;
    display: flex;
    justify-content: center;
  }

  .img{
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .pokeball{
    width: 50px;
    height: 40px;
  }




</style>