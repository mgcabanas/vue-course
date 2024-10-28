<script setup>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue';
import Guitar from './components/Guitar.vue';

const guitars = [
  {
    img: '/img/guitarra_01.jpg',
    nombre: 'Lukather',
    precio: 299
  },
  {
    img: '/img/guitarra_02.jpg',
    nombre: 'SRV',
    precio: 299
  },
  {
    img: '/img/guitarra_03.jpg',
    nombre: 'Borland',
    precio: 299
  },
  {
    img: '/img/guitarra_04.jpg',
    nombre: 'Vai',
    precio: 299
  },
  {
    img: '/img/guitarra_05.jpg',
    nombre: 'Thompson',
    precio: 299
  },
  {
    img: '/img/guitarra_06.jpg',
    nombre: 'White',
    precio: 299
  },
  {
    img: '/img/guitarra_07.jpg',
    nombre: 'Cobain',
    precio: 299
  },
  {
    img: '/img/guitarra_08.jpg',
    nombre: 'Dale',
    precio: 299
  },
  {
    img: '/img/guitarra_09.jpg',
    nombre: 'Krieger',
    precio: 299
  },
  {
    img: '/img/guitarra_10.jpg',
    nombre: 'Campbell',
    precio: 299
  },
  {
    img: '/img/guitarra_11.jpg',
    nombre: 'Reed',
    precio: 299
  },
  {
    img: '/img/guitarra_12.jpg',
    nombre: 'Hazel',
    precio: 299
  },
]
</script>

<template>
<Header />

<main class="container-xl mt-5">
  <h2 class="text-center">Nuestra Colección</h2>

  <div class="row mt-5">
      <Guitar v-for="guitar in guitars" :img="guitar.img" :nombre="guitar.nombre" :precio="guitar.precio" />
  </div>
</main>

<Footer />
</template>
