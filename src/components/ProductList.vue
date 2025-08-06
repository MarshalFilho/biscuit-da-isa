<template>
    <div class="product-list-container">
        <h2>Nossos Produtos</h2>
        <div class="product-grid">
            <ProductCard v-for="produto in produtos" :key="produto.id" :produto="produto" />
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import ProductCard from './ProductCard.vue';

// --- É AQUI QUE VOCÊ ADICIONA OS PRODUTOS ---
// Para adicionar um novo biscuit, basta copiar um dos blocos de objeto e colar,
// alterando os dados (id, nome, preco, imageUrl, shopeeUrl).
const produtos = ref([
    {
        id: 1,
        nome: 'Personagem de Anime em Biscuit',
        preco: 'R$ 80,00',
        imageUrl: 'https://i.imgur.com/ABUI6kj.jpeg', // Use um link de imagem real aqui
        shopeeUrl: 'https://shopee.com.br/seu-link-aqui'
    },
    {
        id: 2,
        nome: 'Vela de Aniversário Temática',
        preco: 'R$ 55,00',
        imageUrl: 'https://i.imgur.com/uSjaFf2.jpeg', // Use um link de imagem real aqui
        shopeeUrl: 'https://shopee.com.br/seu-link-aqui'
    },
    {
        id: 3,
        nome: 'Lembrancinha de Casamento',
        preco: 'A partir de R$ 15,00',
        imageUrl: 'https://i.imgur.com/2s4gwF0.jpeg', // Use um link de imagem real aqui
        shopeeUrl: 'https://shopee.com.br/seu-link-aqui'
    },
    // Adicione mais produtos aqui
]);
</script>

<style scoped>
.product-list-container {
    padding: 2rem 1rem;
    max-width: 1200px;
    margin: 0 auto;
}

h2 {
    text-align: center;
    font-size: 2.5rem;
    margin-bottom: 2rem;
    color: #2c3e50;
}

.product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 2rem;
}
</style>