<script setup lang="ts">
import { ref } from "vue";
import Navbar from "./components/Navbar.vue";
import Results from "./components/Results.vue";
import SearchField from "./components/SearchField.vue";
import { Sorting } from "./types";

const sorting = ref<Sorting>("price-asc");
const query = ref("");
</script>

<template>
  <Navbar v-model:sorting="sorting" />
  <div class="crt-search-container">
    <div class="container-fluid">
      <SearchField v-model:value="query" />
    </div>
  </div>
  <div class="crt-results-container">
    <div class="container-fluid">
      <Results :query="query" :sorting="sorting" />
    </div>
  </div>
</template>
<style>
.crt-search-container {
  background: white;
  padding: 4rem 0;
}

.crt-search-container .crt-search-field {
  max-width: 500px;
  margin: 0 auto;
}

.crt-results-container {
  background: #eee;
  padding: 4rem 0;
  flex-grow: 1;
}

.crt-results-container > div {
  max-width: 960px;
  display: flex;
  flex-direction: column;
  height: 100%;
}
</style>
