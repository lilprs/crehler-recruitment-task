<template>
  <Result
    v-for="result in results"
    :name="result.name"
    :description="result.description"
    :price="result.price"
  />
</template>
<script setup lang="ts">
import Result from "./Result.vue";
const results = [
  {
    name: "Test",
    description: "Test",
    price: 12345,
  },
  {
    name: "Test",
    description: "Test",
    price: 12345,
  },
  {
    name: "Test",
    description: "Test",
    price: 12345,
  },
];
</script>
