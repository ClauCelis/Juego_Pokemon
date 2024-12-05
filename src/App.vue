<template>
  <div id="app">
    <Home />
  </div>
</template>

<script>
import Home from './views/Home.vue';

export default {
  components: {
    Home,
  },
};
</script>

<style>
body {
  background-image: url('./assets/fondo.jpg');
  background-size: cover;
  /* La imagen ocupa todo el fondo */
  background-repeat: no-repeat;
  /* Evita que la imagen se repita */
  background-attachment: fixed;
  /* Fija la imagen al fondo */
  background-position: center;
  /* Centra la imagen */
  margin: 0;
  /* Elimina márgenes para que el fondo cubra toda la ventana */
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #FACC04;

}

h1, h2{
  -webkit-text-stroke: 1px rgb(98, 96, 96);
  /* Añade un borde negro al texto */
}
</style>
