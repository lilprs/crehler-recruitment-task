<script setup lang="ts">
import Navbar from "./components/Navbar.vue";
import SearchField from "./components/SearchField.vue";
</script>

<template>
  <Navbar sorting="price_ascending" />
  <div class="crt-search">
    <SearchField value="" />
  </div>
  <div class="crt-results"></div>
</template>
<style>
.crt-search {
  padding: 5rem;
  background: white;
}

.crt-search > .crt-search-field {
  max-width: 500px;
  margin: 0 auto;
}
</style>
