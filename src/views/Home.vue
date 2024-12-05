<!-- Aquí se carga el componente PokemonList -->
<template>
    <div>
    <img src="../assets/pokemon_logo.png" alt="Pokemon Logo" class="pokemon-logo">
      <h1>¡Adivina el Pokemon!</h1>
      <PokemonList />
    </div>
  </template>
  
  <script>
  import PokemonList from '../components/PokemonList.vue';
  
  export default {
    components: { PokemonList },
  };
  </script>

  <style scoped>
  .pokemon-logo {
    width: 50%;
    margin:0;
    padding: 0;
  }

 
  </style>
  