<template>
    <div class="product-list-container">
        <div class="product-grid-wrapper">
            <h2>Nossos Produtos</h2>

            <div v-if="loading" class="loading-state">
                <div class="spinner"></div>
                <p>Carregando produtos...</p>
            </div>

            <div v-else-if="error" class="error-state">
                <p>Oops! Algo deu errado ao buscar os produtos.</p>
                <p>{{ error }}</p>
            </div>

            <div v-else>
                <div class="filter-container">
                    <button v-for="category in categories" :key="category" @click="selectCategory(category)"
                        :class="{ active: selectedCategory === category }" class="filter-button">
                        {{ category }}
                    </button>
                </div>

                <div v-if="paginatedProdutos.length > 0" class="product-grid">
                    <ProductCard v-for="produto in paginatedProdutos" :key="produto.id" :produto="produto" />
                </div>

                <div v-else class="empty-state">
                    <p>Nenhum produto encontrado na categoria "{{ selectedCategory }}".</p>
                </div>

                <div v-if="hasMoreProducts" class="load-more-container">
                    <button @click="loadMore" class="load-more-button">
                        Carregar Mais
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';
import ProductCard from './ProductCard.vue';

// --- ESTADO DO COMPONENTE ---
const loading = ref(true);
const error = ref(null);
const allProdutos = ref([]); // Armazena TODOS os produtos vindos da "API"

// --- LÓGICA DE FILTRO ---
const selectedCategory = ref('Todos');
const categories = computed(() => {
    const allCategories = allProdutos.value.map(p => p.category);
    return ['Todos', ...new Set(allCategories)];
});

const filteredProdutos = computed(() => {
    if (selectedCategory.value === 'Todos') {
        return allProdutos.value;
    }
    return allProdutos.value.filter(p => p.category === selectedCategory.value);
});

// --- LÓGICA DE PAGINAÇÃO ("CARREGAR MAIS") ---
const itemsPerPage = 6;
const visibleCount = ref(itemsPerPage);

const paginatedProdutos = computed(() => {
    return filteredProdutos.value.slice(0, visibleCount.value);
});

const hasMoreProducts = computed(() => {
    return visibleCount.value < filteredProdutos.value.length;
});

// --- MÉTODOS ---
const selectCategory = (category) => {
    selectedCategory.value = category;
    // Reseta a contagem ao trocar de categoria para uma nova experiência de "Carregar Mais"
    visibleCount.value = itemsPerPage;
};

const loadMore = () => {
    visibleCount.value += itemsPerPage;
};

// --- BUSCA DE DADOS (LIFECYCLE) ---
const fetchProdutos = async () => {
    try {
        await new Promise(resolve => setTimeout(resolve, 1000));
        allProdutos.value = [
            { id: 1, nome: 'Chaveiros de abacate para casal', preco: 8.00, imageUrl: 'https://i.ibb.co/bQdYp2S/chaveiro-abacate.jpg', shopeeUrl: '#', category: 'Chaveiros' },
            { id: 2, nome: 'Chaveiro de Rim Anatômico', preco: 35.00, imageUrl: 'https://i.ibb.co/Bjc12yQ/chaveiro-rim.jpg', shopeeUrl: '#', category: 'Chaveiros' },
            { id: 3, nome: 'Boneca de profissão: Médica', preco: 25.00, imageUrl: 'https://i.ibb.co/fSLGq1b/boneca-medica.jpg', shopeeUrl: '#', category: 'Bonecos de Profissão' },
            { id: 4, nome: 'Boneca de profissão: Advogada', preco: 25.00, imageUrl: 'https://i.ibb.co/JqXb3z5/boneca-advogada.jpg', shopeeUrl: '#', category: 'Bonecos de Profissão' },
            { id: 5, nome: 'Boneca de profissão: Professora', preco: 25.00, imageUrl: 'https://i.ibb.co/L5w2R7v/boneca-professora.jpg', shopeeUrl: '#', category: 'Bonecos de Profissão' },
            { id: 6, nome: 'Chaveiro de Coração', preco: 15.00, imageUrl: 'https://i.ibb.co/YhX34L4/chaveiro-coracao.jpg', shopeeUrl: '#', category: 'Chaveiros' },
            { id: 7, nome: 'Topo de Bolo Casamento', preco: 150.00, imageUrl: 'https://i.ibb.co/3cY0V2d/topo-bolo-casamento.jpg', shopeeUrl: '#', category: 'Topo de Bolo' },
            { id: 8, nome: 'Topo de Bolo Infantil', preco: 80.00, imageUrl: 'https://i.ibb.co/yQJ4T1f/topo-bolo-infantil.jpg', shopeeUrl: '#', category: 'Topo de Bolo' },
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
/* Estilos do Container e Wrapper (com a correção de margem) */
.product-list-container {
    width: 100%;
    padding: 4rem 0;
    background-color: #f7f9fa;
}

.product-grid-wrapper {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
}

/* Título */
h2 {
    text-align: center;
    font-size: 2.5rem;
    margin-bottom: 2rem;
    color: #2c3e50;
    font-family: 'Montserrat', sans-serif;
    font-weight: 600;
}

/* NOVO: Estilos dos Filtros */
.filter-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 1rem;
    margin-bottom: 2.5rem;
}

.filter-button {
    padding: 0.5rem 1.5rem;
    border: 1px solid #ddd;
    background-color: #fff;
    border-radius: 20px;
    cursor: pointer;
    font-family: 'Montserrat', sans-serif;
    font-weight: 600;
    transition: all 0.3s ease;
}

.filter-button:hover {
    background-color: #f0f0f0;
    border-color: #ccc;
}

.filter-button.active {
    background-color: #ee4d2d;
    color: white;
    border-color: #ee4d2d;
}

/* Grade de Produtos */
.product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 2rem;
}

/* NOVO: Estilos do Botão Carregar Mais */
.load-more-container {
    text-align: center;
    margin-top: 2.5rem;
}

.load-more-button {
    padding: 0.8rem 2.5rem;
    border: 2px solid #ee4d2d;
    background-color: transparent;
    color: #ee4d2d;
    border-radius: 8px;
    cursor: pointer;
    font-family: 'Montserrat', sans-serif;
    font-weight: bold;
    font-size: 1rem;
    transition: all 0.3s ease;
}

.load-more-button:hover {
    background-color: #ee4d2d;
    color: white;
}

/* Estilos dos estados (loading, error, empty) */
.loading-state,
.error-state,
.empty-state {
    text-align: center;
    padding: 4rem 1rem;
    color: #6c757d;
    font-family: 'Montserrat', sans-serif;
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