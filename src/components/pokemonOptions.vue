<template>
  <div class="options-container">
      <ul>         
          <li 
                v-for="pokemon in pokemons" 
                :key="pokemon.id" 
                class="correct"
                @click="$emit( 'selection', pokemon.id )">
              {{pokemon.name}}
          </li>
      </ul>
  </div>
</template>

<script>

export default {
    props:{
        pokemons: {
            type: Array,
            required: true
        }
    },
    methods: {
    }
}
</script>

<style scoped>
    ul {
        list-style-type: none;
    }
    li {
        background-color: white;
        border-radius: 5px;
        padding: 5px;
        border: 1px solid rgba(49, 103, 128, 0.609);
        cursor: pointer;
        margin-bottom: 10px;
        width: 250px;
    }

    li:hover {
        background-color: rgba(77, 96, 158, 0.76);
        color: white;
    }

    .options-container {
        display: flex;
        justify-content: center;
    }
</style>