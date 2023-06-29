<template>
  <div class="crt-result">
    <h2>{{ props.name }}</h2>
    <p>{{ props.description }}</p>
    <p><b>Cena</b> {{ props.price }}</p>
  </div>
</template>
<style>
.crt-result {
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  background: white;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
</style>
<script setup lang="ts">
const props = defineProps<{
  name: string;
  description: string;
  price: number;
}>();
</script>
