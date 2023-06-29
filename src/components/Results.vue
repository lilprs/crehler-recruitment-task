<template>
  <Result
    v-for="result in results"
    :name="result.name"
    :description="result.description"
    :price="result.price"
  />
</template>
<script setup lang="ts">
import {
  getCategoryProducts,
  searchProducts,
  setup,
} from "@shopware-pwa/shopware-6-client";
import { onMounted, ref, watch } from "vue";
import Result from "./Result.vue";

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
  sorting: "price_ascending" | "price_descending";
}>();

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
  let raw_result: ShopwareResult = {
    elements: [],
  };

  if (!props.query) {
    raw_result = (await getCategoryProducts(
      "e435c9763b0d44fcab67ea1c0fdb3fa0"
    )) as ShopwareResult; // TODO: fix types from @shopware-pwa/commons
  } else {
    raw_result = await searchProducts({
      query: props.query,
    });
  }

  results.value = raw_result.elements.map((element) => ({
    name: element.translated.name,
    description: element.translated.description,
    price: element.calculatedPrice.totalPrice,
  }));
}

watch(() => props.query, fetch_listing);
onMounted(fetch_listing);
</script>
