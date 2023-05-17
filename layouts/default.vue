<template>
    <Header />

    <slot />

    <Footer />
</template>

<script setup>
import Header from './default/header.vue'
import Footer from './default/footer.vue'
</script>