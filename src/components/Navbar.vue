<template>
  <nav class="navbar bg-dark navbar-expand-lg" data-bs-theme="dark">
    <div class="container-fluid crt-navbar__container">
      <a class="navbar-brand" href="#">Shopware listing</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Przełącz widoczność menu"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <select
          class="form-select w-auto crt-navbar__sorting"
          aria-label="Wybierz sposób sortowania"
          :value="props.sorting"
          @input="(ev) => emit('update:sorting', (ev.target as HTMLSelectElement).value as Sorting)"
        >
          <option value="price-asc">Najtańsze</option>
          <option value="price-desc">Najdroższe</option>
        </select>
      </div>
    </div>
  </nav>
</template>
<style>
.crt-navbar__sorting {
  margin-left: auto;
}
.crt-navbar__container {
  max-width: 960px;
}

.navbar-collapse:is(.show, .collapsing) .crt-navbar__sorting {
  margin-top: 0.5rem;
}
</style>
<script setup lang="ts">
import { Sorting } from "../types";

const props = defineProps<{
  sorting: Sorting;
}>();

const emit = defineEmits<{
  (e: "update:sorting", value: Sorting): void;
}>();
</script>
