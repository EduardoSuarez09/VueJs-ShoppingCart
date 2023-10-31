<script setup>
import { ref, computed } from 'vue';
const header = ref('Mi carrito de compras');
const items = ref([
  {id: 1, label: '10 bolillos', purchased: true, highPriority: true },
  {id: 2, label: '1 lata de frijoles', purchased: false, highPriority: false},
  {id: 3, label: '2 lata de atún', purchased: true, highPriority: false }
]);
//funcion que alterna el estado de comprado de un item
const togglePurchased = (item) => {
  //invertir la propiedad purchased
  item.purchased= !item.purchased;
}
//Agregando metodo para guardar nuevo articulo
const saveItem = () => {
  items.value.push({id: items.value.length + 1, label: newItem.value}) 
//limpiando el contenido de newItem
newItem.value ="";
};
const newItem = ref('');
const newItemHighPriority = ref(false);
const editing = ref (true);
const doEdit = (edit) =>{
  //Altero la variable editing
  editing.value = edit;
  //Limpio el input de texto
  newItem.value = "";
}
//Crando una propiedad computada
const characterCount = computed(()=>{
  // Toda propiedad computada debe regresar un valor
  return newItem.value.length;
});
// Creando propiedad computada que invierte items de la lista
const reversedItems = computed(() => [...items.value].reverse());

</script>


<template>
  <div class="header">
    <h1> <i class="material-icons shopping-cart-icon">local_mall</i> {{ header }}</h1>
    <button v-if ="!editing" @click="doEdit(true)" class="btn btn-primary"> Agregar Articulo</button>
    <button v-else @click="doEdit(false) " class="btn"> Cancelar </button>
  </div>
  <!-- <a :href = "newItem"> 
    <i class ="material-icons shopping-cart-icon"> link </i></a> -->
  <form v-if =" editing " v-on:submit.prevent=" saveItem " class="add-item form">
    <!-- Input de nuevo articulo -->
    <input v-model.trim="newItem" type="text" placeholder="Ingresar nuevo articulo">
    <!-- Check Boxes -->
    <label>
      <input v-model ="newItemHighPriority"
      type="checkbox">
      Alta Prioridad
    </label>
    {{ newItemHighPriority ? "🔥" : "🧊" }}
  <!-- Boton de UI -->
  <button :disabled ="newItem.length==0" class="btn btn-primary"> Salvar Articulo </button>
  	<!-- Contador -->
    <p class="counter">
    {{ characterCount }} / 200
  </p>
  </form>
  <ul>
   <li v-for="({ id, label, purchased, highPriority,  }, index ) in reversedItems" 
   v-bind:key="id"
   :class ="{strikeout : purchased, priority: highPriority} "
   @click="togglePurchased (reversedItems[index])"
   >
    🔹  {{ label }} 
    </li>
  </ul>
  <p v-if="items.length==0" >🥀 Lista de compras vacia 🥀</p>
</template>

<style scoped>
.shopping-cart-icon{
  font-size: 2rem;
}
</style>
