<!-- Este componente manejará la llamada a la API y pasará los datos necesarios a los componentes hijos. -->
<template>
    <div>
      <h2>Pokemones descubiertos: {{ discoveredCount }}</h2>
      <div class="pokemon-list">

        <!-- Renderiza cada Pokémon como una tarjeta -->
        <PokemonCard 
          v-for="pokemon in pokemons" 
          :key="pokemon.name" 
          :pokemon="pokemon" 
          @pokemonDiscovered="incrementCount"
        />
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import PokemonCard from './PokemonCard.vue';
  
  export default {
    components: { PokemonCard },
    data() {
      return {
        pokemons: [], // Lista de pokémones con nombres e imágenes
        discoveredCount: 0, // Contador de pokémones descubiertos
      };
    },
    async mounted() {
      try {
        // Genera 20 IDs aleatorios entre 1 y 1010 (rango válido en la PokéAPI)
        const randomIds = Array.from({ length: 20 }, () => Math.floor(Math.random() * 1010) + 1);
  
        // Hace las solicitudes a la API para los 20 IDs generados
        this.pokemons = await Promise.all(
          randomIds.map(async (id) => {
            const response = await axios.get(`https://pokeapi.co/api/v2/pokemon/${id}`);
            console.log(`Cargando Pokémon ID ${id}:`, response.data.name); // Verifica los datos
            return {
              name: response.data.name, // Nombre del Pokémon
              image: response.data.sprites.front_default, // Imagen del Pokémon
            };
          })
        );
      } catch (error) {
        console.error('Error al cargar los datos de la API:', error);
      }
    },
    methods: {
      incrementCount() {
        this.discoveredCount += 1; // Incrementa el contador de pokémones descubiertos
      },
    },
  };
  </script>
  
  <style>
  .pokemon-list {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
  }
  </style>
  