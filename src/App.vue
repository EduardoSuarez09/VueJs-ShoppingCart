<script setup>
import { ref } from 'vue';
const header = ref('Mi carrito de compras');
const items = ref([
  {id: 1, label: '10 bolillos'},
  {id: 2, label: '1 lata de frijoles'},
  {id: 3, label: '2 lata de atún'}
]);
</script>


<template>
<h1>{{ header }}</h1>
<ul>
  <li v-for="({ id, label } ) in items" v-bind:key="id">
    🔹  {{ label }}
  </li>
</ul>
</template>

<style scoped>
.shopping-cart-icon{
  font-size: 2rem;
}
</style>
