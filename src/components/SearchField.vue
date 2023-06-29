<template>
  <input
    :value="props.value"
    @input="(ev) => emit('update:value', (ev.target as HTMLSelectElement).value)"
    type="text"
    class="form-control crt-search-field"
    placeholder="Wpisz szukaną frazę..."
  />
</template>
<style>
.crt-search-field {
  font-size: 2rem;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}
</style>
<script setup lang="ts">
const props = defineProps<{
  value: string;
}>();

const emit = defineEmits<{
  (e: "update:value", value: string): void;
}>();
</script>
