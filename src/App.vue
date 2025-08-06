<template>
    <TheHeader />
    <main>
        <ProductList />
    </main>
    <TheFooter />
</template>

<script setup>
import TheHeader from './components/TheHeader.vue';
import ProductList from './components/ProductList.vue';
import TheFooter from './components/TheFooter.vue';
</script>

<style>
/* Importando os estilos globais de assets/main.css */
@import './assets/main.css';

main {
    flex: 1;
}
</style>