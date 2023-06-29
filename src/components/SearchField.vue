<template>
  <input
    :value="props.value"
    @input="(ev) => emit('update:value', (ev.target as HTMLSelectElement).value)"
    type="text"
    class="form-control crt-search-field cr-elevated"
    placeholder="Szukaj..."
  />
</template>
<style>
.crt-search-field {
  font-size: 1.5rem;
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
