<template>
    <div class="product-card">
        <img :src="produto.imageUrl" :alt="produto.nome" class="product-image" />
        <div class="product-info">
            <h3 class="product-name">{{ produto.nome }}</h3>
            <p class="product-price">{{ produto.preco }}</p>
            <a :href="produto.shopeeUrl" target="_blank" rel="noopener noreferrer" class="shopee-button">
                Ver na Shopee
            </a>
        </div>
    </div>
</template>

<script setup>
defineProps({
    produto: {
        type: Object,
        required: true
    }
});
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
    /* Altura fixa para manter a consistência */
    object-fit: cover;
    /* Garante que a imagem cubra a área sem distorcer */
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
    /* Cor da Shopee */
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