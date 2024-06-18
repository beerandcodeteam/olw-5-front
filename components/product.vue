<template>
  <div class="bg-white">
    <div class="mx-auto max-w-2xl px-4 py-16 sm:px-6 sm:py-24 lg:max-w-7xl lg:px-8">
      <div class="md:flex md:items-center md:justify-between">
        <h2 class="text-2xl font-bold tracking-tight text-gray-900">Trending products</h2>
        <template v-if="showFilter">
          <button
            @click="toggleModal"
            type="submit"
            class=" rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
          Filtrar
          </button>
        </template>
      </div>

      <div class="mt-6 grid grid-cols-2 gap-x-4 gap-y-10 sm:gap-x-6 md:grid-cols-4 md:gap-y-2 lg:gap-x-8">
        <NuxtLink :to="{name: 'product-id', params: {id: product.id}}" v-for="product in products" :key="product.id" class="group relative">
          <div class="h-56 w-full overflow-hidden rounded-md bg-gray-200 group-hover:opacity-75 lg:h-72 xl:h-80">
            <img :src="`${config.public.s3url}/${product.skus[0].images[0].url}`"  class="h-full w-full object-cover object-center" />
          </div>
          <div class="mt-4 flex justify-between">
            <div>
              <h3 class="text-sm text-gray-700">
                <a :href="product.href">
                  <span aria-hidden="true" class="absolute inset-0" />
                  {{ product.name }}
                </a>
              </h3>
            </div>
            <p class="text-sm font-medium text-gray-900">{{ product.skus[0].price }}</p>
          </div>
        </NuxtLink>
      </div>

      <div class="mt-8 text-sm md:hidden">

      </div>
    </div>
  </div>
</template>

<script setup>
const config = useRuntimeConfig()
const props = defineProps({
  products: {type: Array },
  toggleModal: {type: Function},
  showFilter: {type: Boolean, default: false},


})
</script>
