<template>
  <div class="pb-32">
    <div class="h-[50vh] relative">
      <Hero />
    </div>

    <Filters :categories="assessories.categories" :brands="assessories.brands" :filters="filters" :open="open" :toggleModal="toggleModal" :search="search" />

    <Product :products="products.data" :showFilter="true" :toggleModal="toggleModal" />

    <div class="mx-auto max-w-2xl px-4 py-16 sm:px-6 sm:py-24 lg:max-w-7xl lg:px-8">
      <Pagination :links="products.links" :prev-page="products.prev_page_url" :next-page="products.next_page_url" :get-page="getPage" />
    </div>
  </div>
</template>

<style scoped>

</style>
<script setup lang="ts">
import Product from "~/components/product.vue";
import Brands from "~/components/brands.vue";
import Pagination from "~/components/pagination.vue";
import Filters from "~/components/filters.vue";

const config = useRuntimeConfig()

const products = useState('products')
const assessories = useState('assessories')
const filters = useState('filters', () => {
  return {
    name: "",
    category_id: "",
    brand_id: "",
    value_type: "",
    price: "",
  }
})

const open = useState('open', () => false)

await callOnce(async () => {
  products.value = await $fetch(`${config.public.apiUrl}/api/frontend/products`)
  assessories.value = await $fetch(`${config.public.apiUrl}/api/frontend/productAssessories`)
})

const getPage = async (page) => {
  products.value = await $fetch(page, { method: "GET", params: filters.value })
}

const search = async () => {
  products.value = await $fetch(`${config.public.apiUrl}/api/frontend/products`, { method: "GET", params: filters.value })
}

const toggleModal = () => {
  open.value = !open.value
}

</script>
