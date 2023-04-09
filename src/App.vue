<script setup>
import CardPosts from './components/CardPosts.vue';
import ButtonEvent from './components/ButtonEvent.vue';
import { ref } from 'vue'; // Librería para crear las variables reactivas

// Se crean las variables reactivas necesarias para el funcionamiento de la aplicación
const datos = ref([]);
const datosFavoritos = ref([]);
const paginacion = ref(0);
const rango = 5;

// Se utiliza fetch para consumir las apis, también es posible utilizar las funciones async y await para realizar la misma tarea
fetch('https://jsonplaceholder.typicode.com/posts')
  .then(res => res.json())
  .then(json => {
    datos.value = json
  });

// Funciones que definene el comportamiento de la aplicación emitidas del componente padre
const agregarFavorito = index => {
  datosFavoritos.value.push(datos.value[index - 1]);
}
const eliminarFavorito = index => {
  datosFavoritos.value = datosFavoritos.value.filter(datos => datos.id != index);
}
const next = () => {
  if(paginacion.value + rango < datos.value.length){
    paginacion.value+=5
  }
}
const preview = () => {
  if(paginacion.value > 0){
    paginacion.value-=5
  }
}
</script>

<template>
  <div>
    <article class="separator">
      <article class="card-container">
        <header class="card-container__header">
          <h1 class="card-container__title">Lista de Artículos</h1>
        </header>
        <article class="card-container__article">
          <CardPosts v-for="element in datos.slice(paginacion, paginacion + rango)" 
            :key="element.id" 
            :id="element.id" 
            :title="element.title"
            :body="element.body"
            @buttonEvent="agregarFavorito"
            buttonText="Agregar Favorito" >
          </CardPosts>
        </article>
      </article>
      <article class="card-container">
        <header class="card-container__header">
          <h1 class="card-container__title">Lista de Artículos Favoritos</h1>
        </header>
        <article class="card-container__article">
          <CardPosts v-for="element in datosFavoritos" 
            :key="element.id" 
            :id="element.id" 
            :title="element.title"
            :body="element.body"
            @buttonEvent="eliminarFavorito"
            buttonText="Eliminar Favorito" >
          </CardPosts>
        </article>
      </article>
    </article>
    <footer class="footer">
      <ButtonEvent @event="preview" text="Retroceder"/>
      <ButtonEvent @event="next" text="Siguiente"/>
    </footer>
  </div>
</template>

<style lang="scss">
.separator {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0.5rem;
  max-width: 1000px;
  margin: 0 auto;
}

.card-container {
  max-width: 500px;
}

.footer {
  max-width: 1000px;
  margin: 0 auto;
  text-align: end;
}
</style>