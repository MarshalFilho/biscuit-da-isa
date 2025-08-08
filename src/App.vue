<template>
    <SiteHeader />
    <HighlightBanner />
    <main>
        <ProductList />
    </main>
    <SiteFooter />
    <BackToTopButton />
</template>

<script setup>
import TheHeader from './components/TheHeader.vue';
import HighlightBanner from './components/HighlightBanner.vue';
import ProductList from './components/ProductList.vue';
import TheFooter from './components/TheFooter.vue';
import BackToTopButton from './components/BackToTopButton.vue';
</script>

<style>
@import './assets/main.css';

main {
    flex: 1;
}
</style>