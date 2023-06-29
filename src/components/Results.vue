<template>
  <div class="crt-results--loading" v-if="loading">
    <div>
      <div class="spinner-border" role="status">
        <span class="visually-hidden">Ładowanie...</span>
      </div>
    </div>
  </div>
  <div class="crt-results" v-else>
    <Result
      v-for="result in results"
      :name="result.name"
      :description="result.description"
      :price="result.price"
    />
  </div>
</template>
<style>
.crt-results {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1rem;
  flex-grow: 1;
  align-items: flex-start;
}
.crt-results--loading {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-grow: 1;
}
.crt-results--loading > div {
  transform: scale(3);
}
</style>
<script setup lang="ts">
import {
  getCategoryProducts,
  searchProducts,
  setup,
} from "@shopware-pwa/shopware-6-client";
import { debounce } from "lodash-es";
import { onMounted, ref, watch } from "vue";
import Result from "./Result.vue";
import type { Sorting } from "./../types";

const SHOPWARE_ENDPOINT = import.meta.env.VITE_SHOPWARE_ENDPOINT;
const SHOPWARE_ACCESS_TOKEN = import.meta.env.VITE_SHOPWARE_ACCESS_TOKEN;

if (!SHOPWARE_ENDPOINT || !SHOPWARE_ACCESS_TOKEN) {
  throw new Error(
    "Missing Shopware endpoint or access token. Define them in .env file."
  );
}

if (SHOPWARE_ENDPOINT.endsWith("store-api/")) {
  throw new Error(
    "Shopware endpoint should not end with store-api/. Please remove it from .env file."
  );
}

setup({
  endpoint: SHOPWARE_ENDPOINT,
  accessToken: SHOPWARE_ACCESS_TOKEN,
});

const props = defineProps<{
  query: string;
  sorting: Sorting;
}>();

const loading = ref(true);

const results = ref<
  {
    name: string;
    description: string;
    price: number;
  }[]
>([]);

type ShopwareResult = {
  elements: {
    translated: {
      name: string;
      description: string;
    };
    calculatedPrice: {
      totalPrice: number;
    };
  }[];
};

async function fetch_listing() {
  loading.value = true;
  let raw_result: ShopwareResult = {
    elements: [],
  };

  const sorting_options = {
    order: props.sorting,
  };

  if (!props.query) {
    raw_result = await getCategoryProducts(
      "e435c9763b0d44fcab67ea1c0fdb3fa0",
      sorting_options
    );
  } else {
    raw_result = await searchProducts({
      query: props.query,
      ...sorting_options,
    });
  }

  results.value = raw_result.elements.map((element) => ({
    name: element.translated.name,
    description: element.translated.description,
    price: element.calculatedPrice.totalPrice,
  }));
  loading.value = false;
}

const fetch_listing_debounced = debounce(fetch_listing, 500);

watch(() => [props.query, props.sorting], fetch_listing_debounced);
onMounted(fetch_listing_debounced);
</script>
