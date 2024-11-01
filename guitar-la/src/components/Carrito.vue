<script setup>
import { inject, ref, watch } from 'vue';

const total = ref(0);
const estado = ref('El carrito está vacío');
const guitarras = inject('guitarras');
const guitarrasAgregadas = ref([]);

const calcularTotal = () => {
    total.value = guitarrasAgregadas.value.reduce((acc, guitarra) => acc + (guitarra.precio * guitarra.cantidad), 0);
}

const actualizarCarrito = () => {
    guitarrasAgregadas.value = guitarras.value.filter(guitarra => guitarra.cantidad > 0);

    if(guitarrasAgregadas.value.length > 0) {
        estado.value = 'Guitarras agregadas al carrito';
    } else {
        estado.value = 'El carrito está vacío';
    }
}

const eliminarDelCarrito = (guitarra) => {
    guitarra.cantidad = 0;
    actualizarCarrito();
    calcularTotal();
}

const vaciarCarrito = () => {
    guitarras.value.forEach(guitarra => guitarra.cantidad = 0);
}

watch(guitarras, () => {
    actualizarCarrito();
    calcularTotal();
}, { deep: true })

actualizarCarrito();
calcularTotal();

</script>

<template>
<div class="carrito">
    <img class="img-fluid" src="/img/carrito.png" alt="imagen carrito" />

    <div id="carrito" class="bg-white p-3">
        <p class="text-center">{{ estado }}</p>
        <table v-if="guitarrasAgregadas.length > 0" class="w-100 table">
            <thead>
                <tr>
                    <th>Imagen</th>
                    <th>Nombre</th>
                    <th>Precio</th>
                    <th>Cantidad</th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="guitarra in guitarrasAgregadas">
                    <td>
                        <img class="img-fluid" :src="`/img/${guitarra.imagen}.jpg`" alt="imagen guitarra">
                    </td>
                    <td>{{ guitarra.nombre }}</td>
                    <td class="fw-bold">{{ `$${guitarra.precio}` }}</td>
                    <td class="flex align-items-start gap-4">
                        <button type="button" class="btn btn-dark" @click="guitarra.cantidad > 1 ? guitarra.cantidad-- : guitarra.cantidad"> - </button>
                        {{ guitarra.cantidad }}
                        <button type="button" class="btn btn-dark" @click="guitarra.cantidad++"> + </button>
                    </td>
                    <td>
                        <button class="btn btn-danger" type="button" @click="eliminarDelCarrito(guitarra)"> X </button>
                    </td>
                </tr>
            </tbody>
        </table>

        <p v-if="guitarrasAgregadas.length > 0" class="text-end">Total pagar: <span class="fw-bold">{{ `$${total}` }}</span></p>
        <button v-if="guitarrasAgregadas.length > 0" class="btn btn-dark w-100 mt-3 p-2" @click="vaciarCarrito">Vaciar Carrito</button>
    </div>
</div>
</template>