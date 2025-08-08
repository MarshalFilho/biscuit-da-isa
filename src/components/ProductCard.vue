<template>
    <div class="product-card">
        <img :src="produto.imageUrl" :alt="produto.nome" class="product-image" @error="onImageError" />
        <div class="product-info">
            <h3 class="product-name">{{ produto.nome }}</h3>
            <p class="product-price">A partir de {{ formattedPrice }}</p>
            <div text-align="center">
                <a :href="produto.shopeeUrl" target="_blank" rel="noopener noreferrer" class="shopee-button"
                    :aria-label="`Ver ${produto.nome} na Shopee`">
                    Ver na Shopee
                </a>
            </div>
        </div>
    </div>
</template>

<script setup>
import { computed } from 'vue';
const props = defineProps({
    produto: {
        type: Object,
        required: true
    }
});

const formattedPrice = computed(() => {
    if (typeof props.produto.preco !== 'number') {
        return props.produto.preco;
    }
    return new Intl.NumberFormat('pt-BR', {
        style: 'currency',
        currency: 'BRL'
    }).format(props.produto.preco);
});

const onImageError = (event) => {
    event.target.src = 'https://placehold.co/400x250?text=Imagem+Indisponível';
};
</script>

<style scoped>
.product-card {
    background-color: #ffffff;
    border-radius: 12px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    overflow: hidden;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    display: flex;
    flex-direction: column;
}

.product-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.12);
}

.product-image {
    width: 100%;
    height: 250px;
    object-fit: cover;
    background-color: #f0f0f0;
    /* Cor de fundo enquanto a imagem carrega */
}

.product-info {
    padding: 1.5rem;
    text-align: center;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.product-name {
    font-size: 1.25rem;
    font-weight: 600;
    margin: 0 0 0.5rem 0;
    color: #333;
}

.product-price {
    font-size: 1.1rem;
    color: #666;
    margin: 0 0 1rem 0;
}

.shopee-button {
    display: inline-block;
    background-color: #ee4d2d;
    color: white;
    padding: 0.75rem 1.5rem;
    border-radius: 8px;
    text-decoration: none;
    font-weight: bold;
    transition: background-color 0.3s ease;
}

.shopee-button:hover {
    background-color: #d73112;
}
</style>