<template>
  <div>
    <h1>{{ nombreLista }}</h1>
    <ul>
      <li v-for="(quehacer, index) in queHaceres" :key="index">
        {{ quehacer.name }}
        <button @click="eliminarQuehacer(index)">Eliminar</button>
        <button @click="editarQuehacer(index)">Editar</button>
      </li>
    </ul>
    <input type="text" v-model="nuevaTarea" @keyup.enter="agregarQuehacer">
    <button @click="agregarQuehacer">Agregar Tarea</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const nombreLista = ref('Tareas Pendientes');
const queHaceres = ref([
    {
        name: "Cocinar",
    },
    {
        name: "Limpiar",
    },
    {
        name: "Barrer",
    },
]);
const nuevaTarea = ref('');

function agregarQuehacer() {
    if (nuevaTarea.value.trim() !== '') {
        queHaceres.value.push({ name: nuevaTarea.value });
        nuevaTarea.value = '';
    }
}

function eliminarQuehacer(index) {
    queHaceres.value.splice(index, 1);
}

function editarQuehacer(index) {
    const nuevoNombre = prompt("Ingrese el nuevo nombre:");
    if (nuevoNombre && nuevoNombre.trim() !== '') {
        queHaceres.value[index].name = nuevoNombre;
    }
}
</script>

<style>
h1 {
  color: red;
}
</style>