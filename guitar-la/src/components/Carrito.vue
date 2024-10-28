<script setup>
import { onMounted, ref } from 'vue';

const props = defineProps({
    guitarras: Array
})

const total = ref(0);

onMounted(() => {
    total.value = guitarras?.reduce((acc, guitarra) => acc + guitarra.precio * guitarra.cantidad, 0)
})

const estado = 'El carrito está vacío'
</script>

<template>
<div class="carrito">
    <img class="img-fluid" src="/img/carrito.png" alt="imagen carrito" />

    <div id="carrito" class="bg-white p-3">
        <p class="text-center">{{ estado }}</p>
        <table class="w-100 table">
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
                <tr v-for="guitarra in guitarras">
                    <td>
                        <img class="img-fluid" :src="guitarra.img" alt="imagen guitarra">
                    </td>
                    <td>{{ guitarra.nombre }}</td>
                    <td class="fw-bold">{{ `$${guitarra.precio}` }}</td>
                    <td class="flex align-items-start gap-4">
                        <button type="button" class="btn btn-dark"> - </button>
                        {{ guitarra.cantidad }}
                        <button type="button" class="btn btn-dark"> + </button>
                    </td>
                    <td>
                        <button class="btn btn-danger" type="button"> X </button>
                    </td>
                </tr>
            </tbody>
        </table>

        <p class="text-end">Total pagar: <span class="fw-bold">{{ `$${total}` }}</span></p>
        <button class="btn btn-dark w-100 mt-3 p-2">Vaciar Carrito</button>
    </div>
</div>
</template>