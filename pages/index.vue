<template>
  <template>
    <div class="h-[50vh] relative">
      <Hero />
    </div>
    <brands :brands="data.brands" />
    <Product :products="data.products" />

  </template>
</template>

<style scoped>

</style>
<script setup lang="ts">
import Product from "~/components/product.vue";
import Brands from "~/components/brands.vue";
import Filters from "~/components/filters.vue";
const config = useRuntimeConfig()
const { data } =  await useFetch(`${config.public.apiUrl}/api/frontend/home`)

</script>
