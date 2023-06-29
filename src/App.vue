<script setup lang="ts">
import Navbar from "./components/Navbar.vue";
import Results from "./components/Results.vue";
import SearchField from "./components/SearchField.vue";
</script>

<template>
  <Navbar sorting="price_ascending" />
  <div class="crt-search">
    <div class="container-fluid">
      <SearchField value="" />
    </div>
  </div>
  <div class="crt-results">
    <div class="container-fluid">
      <Results query="" />
    </div>
  </div>
</template>
<style>
.crt-search {
  background: white;
  padding: 4rem 0;
}

.crt-search .crt-search-field {
  max-width: 500px;
  margin: 0 auto;
}

.crt-results {
  background: #eee;
  padding: 4rem 0;
}

.crt-results > div {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1rem;
  flex-grow: 1;
  align-items: flex-start;
  max-width: 960px;
}
</style>
