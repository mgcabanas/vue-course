<script setup>
import { ref, watch, onMounted } from 'vue';
import Header from './components/Header.vue'
import Footer from './components/Footer.vue';
import Guitar from './components/Guitar.vue';
import {db} from './assets/data/guitarras.js';

const guitarras = ref(db.map((guitarra) => {
    return {
        id: guitarra.id,
        nombre: guitarra.nombre,
        precio: guitarra.precio,
        descripcion: guitarra.descripcion, 
        imagen: guitarra.imagen,
        cantidad: 0,
    }
}));
const carrito = ref([]);

const agregarEnCarrito = (guitarra) => {
    const guitarraEnCarrito = carrito.value.find(_guitarra => _guitarra.id === guitarra.id);
    if(!guitarraEnCarrito)
        carrito.value.push({...guitarra, cantidad: 1}) 
}

const eliminarDeCarrito = (guitarra) => {
    carrito.value = carrito.value.filter(_guitarra => _guitarra.id !== guitarra.id);
}

const vaciarCarrito = () => {
    carrito.value = [];
}

// Obtener el valor del carrito desde localstorage
onMounted(() => {
    carrito.value = JSON.parse(localStorage.getItem('carrito') || [])
})

// Guardar en localstorage el valor del carrito
watch(carrito, () => {
    localStorage.setItem('carrito', JSON.stringify(carrito.value));
}, { deep: true })

</script>

<template>
<Header :guitarras="guitarras" 
        :carrito="carrito" 
        @agregar-en-carrito="agregarEnCarrito" 
        @eliminar-carrito="eliminarDeCarrito" 
        @vaciar-carrito="vaciarCarrito"
/>

<main class="container-xl mt-5">
  <h2 class="text-center">Nuestra Colección</h2>

  <div class="row mt-5">
      <Guitar v-for="guitarra in guitarras" :guitarra="guitarra" @agregar-en-carrito="agregarEnCarrito"/>
  </div>
</main>

<Footer />
</template>
