<template>
    <footer class="site-footer">
        <p>&copy; {{ currentYear }} - Biscuit da Isa. Todos os direitos reservados.</p>
        <p>Entre em contato pelo <a href="https://wa.me/556298529" target="_blank">WhatsApp</a>!</p>
    </footer>
</template>

<script setup>
const currentYear = new Date().getFullYear();
</script>

<style scoped>
.site-footer {
    text-align: center;
    padding: 2rem 1rem;
    margin-top: 2rem;
    background-color: #343a40;
    color: #f8f9fa;
}

.site-footer a {
    color: #17a2b8;
    text-decoration: none;
}

.site-footer a:hover {
    text-decoration: underline;
}
</style>