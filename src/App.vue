<script setup>
import { ref } from 'vue';
const cart = ref([]);
</script>

<template>
  <main class="mx-auto max-w-5xl p-8">
    <h1 class="text-2xl font-semibold">Contoso Store</h1>
    <p class="text-sm text-slate-500">{{ cart.length }} items in cart</p>
  </main>
</template>
