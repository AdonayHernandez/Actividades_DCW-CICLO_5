<script setup>
import { ref, computed } from 'vue';

const primerNombre = ref('Adonay');
const primerApellido = ref('Hernández');
const nombre = ref('');

const NombreEnMayusculas =computed({
  get: () => nombre.value.toUpperCase(),
  set: (nombreNuevo) => {
    nombre.value = nombreNuevo.toLowerCase();
  }

})

const NombreCompleto = computed(() => {
  return `${primerNombre.value} ${primerApellido.value}`;
})


const productos = ref([
  {   nombre: 'Laptop', disponible: true },
  {   nombre: 'Mouse', disponible: false },
  {   nombre: 'Teclado', disponible: true },
])

const disponibles = computed(() => {
  return productos.value.filter(p => p.disponible);
})

const carrito = ref([
  { producto: 'Camisa', precio: 20 ,cantidad: 2},
  { producto: 'Pantalon', precio: 25, cantidad: 5 },
  { producto: 'Calceta', precio: 5, cantidad: 10 },
  
])
const totalCarrito = computed(() => {
  return carrito.value.reduce((acc , item) => acc + item.precio * item.cantidad, 0);
})

</script>

<template>
  <div class="fixed top-0 left-0 w-64 p-4 bg-gray-100">
    <h1 class="text-xl font-bold mb-4">Nombre Completo: {{ NombreCompleto }}</h1>

    <h2 class="text-lg font-semibold mb-2">productos disponibles:</h2>
    <ul class="space-y-2">
      <li v-for="producto in disponibles" 
          :key="producto.nombre"
          class="text-gray-700">
        {{ producto.nombre }}
      </li>
    </ul>
    <br>
    <h1>Total a pagar: {{ totalCarrito }}</h1>
    
    <br>

    <input v-model="NombreEnMayusculas" />
    <p>Nombre: original: {{ nombre }} </p>
  </div>
</template>