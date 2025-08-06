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
        nome: 'Chaveiros de biscuit para casal ou amigos',
        preco: 'A partir de R$ 8,00',
        imageUrl: 'https://down-br.img.susercontent.com/file/8801580a783d724ccba147368130b0cf.webp', // Use um link de imagem real aqui
        shopeeUrl: 'https://shopee.com.br/Chaveiros-de-biscuit-para-casal-ou-amigos-i.409141199.10010613388'
    },
    {
        id: 2,
        nome: 'Chaveiro de Rim e Pulmão',
        preco: 'A partir de R$ 35,00',
        imageUrl: 'https://down-br.img.susercontent.com/file/f7dcb211efa77de881e77ac5694617b6.webp', // Use um link de imagem real aqui
        shopeeUrl: 'https://shopee.com.br/Chaveiro-de-Rim-e-pulm%C3%A3o-20-unidades-i.409141199.12611059154'
    },
    {
        id: 3,
        nome: 'Bonecos de profissões, biscuit personalizados',
        preco: 'A partir de R$ 25,00',
        imageUrl: 'https://down-br.img.susercontent.com/file/62595e118fc8b7ef283dcf6dfd3ded8b.webp', // Use um link de imagem real aqui
        shopeeUrl: 'https://shopee.com.br/Bonecos-de-profiss%C3%B5es-biscuit-personalizados-i.409141199.4093389565'
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