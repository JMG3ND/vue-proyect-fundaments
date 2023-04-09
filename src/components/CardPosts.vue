<script setup>
import ButtonEvent from './ButtonEvent.vue';
// Se definen los props con la función defineProps
// Estos props pueden definirse como un arreglo de Strings o como un objeto
const props = defineProps({
    id: Number,
    title: String,
    body: String,
    buttonText: String
})

// Se encapsula el evento recibido del elemento padre para poder utilizarlo en el componente button
const events = defineEmits(['buttonEvent'])
const secundaryEvent = () => {
    events('buttonEvent', props.id)
}
</script>

<template>
    <section class="card">
        <header class="card__header">
            <h2 class="card__title">{{ id }}. {{ title }}</h2>
        </header>
        <article class="card__article">{{ body }}</article>
        <footer class="card__footer">
            <ButtonEvent @event="secundaryEvent" :text="buttonText" />
        </footer>
    </section>
</template>

<style lang="scss">
.card {
    background-color: rgb(205, 205, 205);
    padding: 1rem;
    margin-bottom: 0.5rem;
    border-radius: 10px;

    &__footer {
        text-align: end;
        margin-top: 1rem;
    }
}
</style>