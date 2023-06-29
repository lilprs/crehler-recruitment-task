<script setup lang="ts">
import Navbar from "./components/Navbar.vue";
import Results from "./components/Results.vue";
import SearchField from "./components/SearchField.vue";
</script>

<template>
  <Navbar sorting="price_ascending" />
  <div class="crt-search">
    <SearchField value="" />
  </div>
  <div class="crt-results">
    <Results />
  </div>
</template>
<style>
.crt-search {
  padding: 1rem;
  background: white;
}

.crt-search > .crt-search-field {
  max-width: 500px;
  margin: 0 auto;
}

.crt-results {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 1rem;
  padding: 1rem;
  background: #eee;
  flex-grow: 1;
  align-items: flex-start;
}

@media (min-width: 700px) {
  .crt-search,
  .crt-results {
    padding: 5rem;
  }
}
</style>
