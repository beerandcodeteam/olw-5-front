<template>
  <nav class="flex items-center justify-between border-t border-gray-200 px-4 sm:px-0">
    <div class="-mt-px flex w-0 flex-1">
      <a @click="() => getPage(prevPage)" class="cursor-pointer inline-flex items-center border-t-2 border-transparent pr-1 pt-4 text-sm font-medium text-gray-500 hover:border-gray-300 hover:text-gray-700">
        <ArrowLongLeftIcon class="mr-3 h-5 w-5 text-gray-400" aria-hidden="true" />
        Previous
      </a>
    </div>
    <div class="hidden md:-mt-px md:flex">
      <template v-for="(link, index) in links" :key="`link-${link.label}`">
        <template v-if="index !== 0 && index !== links.length - 1">
        <a @click="() => getPage(link.url)" class="cursor-pointer inline-flex items-center border-t-2 border-transparent px-4 pt-4 text-sm font-medium text-gray-500 hover:border-gray-300 hover:text-gray-700">{{ link.label }}</a>
        </template>
      </template>
    </div>
    <div class="-mt-px flex w-0 flex-1 justify-end">
      <a @click="() => getPage(nextPage)" class="cursor-pointer inline-flex items-center border-t-2 border-transparent pl-1 pt-4 text-sm font-medium text-gray-500 hover:border-gray-300 hover:text-gray-700">
        Next
        <ArrowLongRightIcon class="ml-3 h-5 w-5 text-gray-400" aria-hidden="true" />
      </a>
    </div>
  </nav>
</template>

<script setup>
import { ArrowLongLeftIcon, ArrowLongRightIcon } from '@heroicons/vue/20/solid'

const props = defineProps({
  getPage: {type: Function, required: true},
  links: {type: Array },
  prevPage: {type: String },
  nextPage: {type: String }
})

</script>
