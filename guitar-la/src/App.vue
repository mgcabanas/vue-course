<script setup>
import { provide, ref } from 'vue';
import Header from './components/Header.vue'
import Footer from './components/Footer.vue';
import Guitar from './components/Guitar.vue';
import {db} from './assets/data/guitarras.js';

const datosMapeados = db.map((guitarra) => {
    return {
        id: guitarra.id,
        nombre: guitarra.nombre,
        precio: guitarra.precio,
        descripcion: guitarra.descripcion, 
        imagen: guitarra.imagen,
        cantidad: 0,
    }
})
const guitarras = ref(datosMapeados);

provide('guitarras', guitarras);

</script>

<template>
<Header />

<main class="container-xl mt-5">
  <h2 class="text-center">Nuestra Colección</h2>

  <div class="row mt-5">
      <Guitar v-for="guitarra in guitarras" :guitarra="guitarra" />
  </div>
</main>

<Footer />
</template>
