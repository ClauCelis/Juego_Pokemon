<!-- Este componente gestiona la lógica para verificar si el usuario adivinó el nombre del Pokémon -->
<template>
    <div class="pokemon-card">
        <!-- Imagen del Pokémon con clases dinámicas para manejar el filtro -->
        <img :src="pokemonImage" :class="{ discovered: isDiscovered, hidden: !isDiscovered }" alt="Pokemon"
            class="pokemon-image" />

        <!-- Input para adivinar el Pokémon, aparece si no ha sido descubierto -->
        <div v-if="!isDiscovered">
            <!-- Caja de entrada para el nombre del Pokémon -->
            <input v-model="userInput" placeholder="¿Quién es este Pokemon?" class="pokemon-input" />
            <!-- Botón para enviar el intento -->
            <button @click="checkName" class="pokemon-button">Descubrir</button>

            <!-- Mensaje de error si el nombre es incorrecto -->
            <p v-if="showError" class="error-message">Nombre incorrecto. Intenta de nuevo.</p>
        </div>

        <!-- Muestra el nombre del Pokémon si ya ha sido descubierto -->
        <div v-else>
            <p class="pokemon-name">{{ pokemon.name }}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: ['pokemon'], // Recibe el Pokémon desde el componente padre
    data() {
        return {
            isDiscovered: false, // Indica si el Pokémon ha sido descubierto
            userInput: '', // Almacena el texto ingresado por el usuario
            showError: false, // Controla si se muestra el mensaje de error
        };
    },
    computed: {
        // Retorna la URL de la imagen del Pokémon
        pokemonImage() {
            return this.pokemon.image;
        },
    },
    methods: {
        // Verifica si el nombre ingresado coincide con el nombre real del Pokémon
        checkName() {
            if (this.userInput.toLowerCase() === this.pokemon.name.toLowerCase()) {
                this.isDiscovered = true; // Marca el Pokémon como descubierto
                this.showError = false; // Oculta el mensaje de error
                this.$emit('pokemonDiscovered'); // Notifica al padre que se descubrió un Pokémon
            } else {
                this.showError = true; // Muestra el mensaje de error
            }
        },
    },
};
</script>

<style scoped>
/* Estilo para la tarjeta del Pokémon */
.pokemon-card {
    text-align: center;
    margin: 20px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 8px;
    background-color: #f9f9f9;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

/* Estilo para la imagen del Pokémon */
.pokemon-image {
    width: 150px;
    height: 150px;
    margin-bottom: 10px;
    transition: filter 0.3s ease;
    /* Suaviza la transición al quitar el filtro */
}

/* Clase para la imagen descubierta */
.discovered {
    filter: none;
    /* Elimina el blur y el efecto de escala de grises */
}

/* Clase para la imagen oculta */
.hidden {
    filter: blur(5px) grayscale(100%);
}

/* Estilo del input */
.pokemon-input {
    width: 80%;
    padding: 8px;
    margin-bottom: 10px;
    /* Asegura que el input esté encima del botón */
    border: 1px solid #ccc;
    border-radius: 4px;
}

/* Estilo del botón */
.pokemon-button {
    padding: 8px 16px;
    background-color: #4caf50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

/* Estilo del mensaje de error */
.error-message {
    color: red;
    font-size: 0.9em;
    margin-top: 10px;
}

/* Estilo del nombre del Pokémon */
.pokemon-name {
    font-size: 1.2em;
    font-weight: bold;
    color: #333;
}
</style>