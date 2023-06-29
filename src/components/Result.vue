<template>
  <div class="crt-result">
    <h2 class="crt-result__name">{{ props.name }}</h2>
    <p class="crt-result__description">
      {{
        props.description.substring(0, 300) +
        (props.description.length > 300 ? "..." : "")
      }}
    </p>
    <p class="crt-result__price">
      <b>Cena</b> {{ currency_formatter.format(props.price) }}
    </p>
  </div>
</template>
<style>
.crt-result {
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  background: white;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.crt-result__name {
  font-size: 1.5rem;
  margin: 0;
}

.crt-result__price {
  font-size: 1.5rem;
  margin: 0;
}

.crt-result__description {
  font-size: 0.9rem;
  margin: 0;
}
</style>
<script setup lang="ts">
const props = defineProps<{
  name: string;
  description: string;
  price: number;
}>();

const currency_formatter = new Intl.NumberFormat("pl-PL", {
  style: "currency",
  currency: "PLN",
});
</script>
