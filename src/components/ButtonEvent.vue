<script setup>
// Este componente utiliza el $emit para recibir los eventos proporcionados por el componente padre
// Cabe recalcar que estos eventos se pueden definir en el script con la función 'defineEmits()' que recibe como parámetro un arreglo de strings
// Ejemplo para este componente
// defineEmits(['preview', next]) //cabe recalcar que este método devuelve el arreglo lo que permite almacenarlo en una variable y utilizar los métodos en el script
defineProps(['text'])
</script>

<template>
    <button @click="$emit('event')" class="button-event">
        {{ text }}
    </button>
</template>

<style lang="scss">
.button-event {
    display: inline-block;
    padding: 0.5rem;
    border: none;
    border-radius: 10px;
    cursor: pointer;

    &:hover {
        background-color: rgb(148, 148, 148);
    }
}
</style>