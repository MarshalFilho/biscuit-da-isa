<template>
    <div class="product-list-container">
        <h2>Nossos Produtos</h2>

        <div v-if="loading" class="loading-state">
            <div class="spinner"></div>
            <p>Carregando produtos...</p>
        </div>

        <div v-else-if="error" class="error-state">
            <p>Oops! Algo deu errado ao buscar os produtos.</p>
            <p>{{ error }}</p>
        </div>

        <div v-else-if="produtos.length > 0" class="product-grid">
            <ProductCard v-for="produto in produtos" :key="produto.id" :produto="produto" />
        </div>
        <div v-else class="empty-state">
            <p>Nenhum produto encontrado no momento.</p>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import ProductCard from './ProductCard.vue';

const produtos = ref([]);
const loading = ref(true);
const error = ref(null);

const fetchProdutos = async () => {
    try {
        await new Promise(resolve => setTimeout(resolve, 2000));

        produtos.value = [
            {
                id: 1,
                nome: 'Chaveiros de biscuit para casal ou amigos',
                preco: 8.00,
                imageUrl: 'https://down-br.img.susercontent.com/file/8801580a783d724ccba147368130b0cf.webp',
                shopeeUrl: 'https://shopee.com.br/Chaveiros-de-biscuit-para-casal-ou-amigos-i.409141199.10010613388'
            },
            {
                id: 2,
                nome: 'Chaveiro de Rim e Pulmão',
                preco: 35.00,
                imageUrl: 'https://down-br.img.susercontent.com/file/f7dcb211efa77de881e77ac5694617b6.webp',
                shopeeUrl: 'https://shopee.com.br/Chaveiro-de-Rim-e-pulm%C3%A3o-20-unidades-i.409141199.12611059154'
            },
            {
                id: 3,
                nome: 'Bonecos de profissões, biscuit personalizados',
                preco: 25.00,
                imageUrl: 'https://down-br.img.susercontent.com/file/62595e118fc8b7ef283dcf6dfd3ded8b.webp',
                shopeeUrl: 'https://shopee.com.br/Bonecos-de-profiss%C3%B5es-biscuit-personalizados-i.409141199.4093389565'
            },
        ];

    } catch (e) {
        error.value = e.message || 'Não foi possível carregar os dados.';
    } finally {
        loading.value = false;
    }
};
onMounted(() => {
    fetchProdutos();
});
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

.loading-state,
.error-state,
.empty-state {
    text-align: center;
    padding: 4rem 1rem;
    color: #6c757d;
}

.spinner {
    margin: 0 auto 1rem;
    border: 4px solid rgba(0, 0, 0, 0.1);
    width: 36px;
    height: 36px;
    border-radius: 50%;
    border-left-color: #ee4d2d;
    animation: spin 1s ease infinite;
}

@keyframes spin {
    0% {
        transform: rotate(0deg);
    }

    100% {
        transform: rotate(360deg);
    }
}
</style>