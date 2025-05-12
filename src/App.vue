<script setup>
import { onMounted, reactive, ref } from 'vue';

// logique de composant
const nom = ref('Khun');
const lien = '<a href="https://google.be">Lien vers Google</a>';
const disabled = true;

const score = ref(4);

onMounted(() => {
    setTimeout(() => {
        nom.value = 'Aude';
        console.log(nom.value);
        // movies.splice(1, 1);
        movies.unshift({ id: 4, title: 'Jurassic Park' });
    }, 2000);
})

const movies = reactive([
    { id: 1, title: 'E.T.'},
    { id: 2, title: 'The Matrix'},
    { id: 3, title: 'The Lord of the Rings'},
])

const changeName = () => {
    nom.value = 'Georges';
} 
</script>

<template>
    <!-- html du composant -->
    <p :class="{
        success: score > 5,
        danger: score <= 5
    }">Hello {{ nom }} !</p>
    <p>{{ lien }}</p>
    <p v-html="lien"></p>
    <button :disabled="disabled">Click me !!</button>
    <ul>
        <li v-for="item in movies" :key="item.id">{{ item.title }}</li>
    </ul>
    <button @click="changeName()">Click me !!</button>
</template>

<style scoped>
/* style du composant */
.success {
    color: green;
}
.danger {
    color: red;
}

@keyframes app {
    0% { opacity: 0; transform: translateX(-50px); }
    100% { opacity: 1; transform: translateX(0); }
}

li {
    animation: app 1s ease; 
}
</style>