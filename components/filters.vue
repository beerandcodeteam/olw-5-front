<template>
  <TransitionRoot as="template" :show="open">
    <Dialog class="relative z-20" @close="open = false">
      <div class="fixed inset-0" />

      <div class="fixed inset-0 overflow-hidden">
        <div class="absolute inset-0 overflow-hidden">
          <div class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10">
            <TransitionChild as="template" enter="transform transition ease-in-out duration-500 sm:duration-700" enter-from="translate-x-full" enter-to="translate-x-0" leave="transform transition ease-in-out duration-500 sm:duration-700" leave-from="translate-x-0" leave-to="translate-x-full">
              <DialogPanel class="pointer-events-auto w-screen max-w-md">
                <div class="flex h-full flex-col overflow-y-scroll bg-white py-6 shadow-xl">
                  <div class="px-4 sm:px-6">
                    <div class="flex items-start justify-between">
                      <DialogTitle class="text-base font-semibold leading-6 text-gray-900">Filtros</DialogTitle>
                      <div class="ml-3 flex h-7 items-center">
                        <button type="button" class="relative rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2" @click="toggleModal">
                          <span class="absolute -inset-2.5" />
                          <span class="sr-only">Close panel</span>
                          <XMarkIcon class="h-6 w-6" aria-hidden="true" />
                        </button>
                      </div>
                    </div>
                  </div>

                  <div class="relative mt-6 flex-1 px-4 sm:px-6">
                    <div class="sm:col-span-4">
                      <label for="country" class="block text-sm font-medium leading-6 text-gray-900">Categoria</label>
                      <div class="mt-2">
                        <select
                          v-model="filters.category_id"
                          class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6" >
                          <option value="">Selecione</option>
                          <template v-for="category in categories">
                            <option :value="category.id">{{ category.name }}</option>
                          </template>
                        </select>
                      </div>
                    </div>

                    <div class="sm:col-span-4 mt-4">
                      <label for="country" class="block text-sm font-medium leading-6 text-gray-900">Marcas</label>
                      <div class="mt-2">
                        <select
                          v-model="filters.brand_id"
                          class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6" >
                          <option value="">Selecione</option>
                          <template v-for="brand in brands">
                            <option :value="brand.id">{{ brand.name }}</option>
                          </template>
                        </select>
                      </div>
                    </div>


                    <div class="sm:col-span-4  mt-4">
                      <label for="email" class="block text-sm font-medium leading-6 text-gray-900">Busque por valor</label>
                      <select
                        v-model="filters.value_type"
                        class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6" >
                        <option value="">Selecione</option>
                        <option value="<">Menor que</option>
                        <option value=">">Maior que</option>
                      </select>

                      <label for="value" class="block text-sm font-medium leading-6 text-gray-900">Valor</label>
                      <div class="mt-2">
                        <input v-model="filters.price" id="value" name="value" type="number" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
                      </div>
                    </div>

                    <div class="mt-6 flex items-center justify-end gap-x-6">
                      <button @click="toggleModal" type="button" class="text-sm font-semibold leading-6 text-gray-900">Cancel</button>
                      <button @click="search" type="submit" class="rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">buscar</button>
                    </div>
                  </div>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup>
import { ref } from 'vue'
import { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from '@headlessui/vue'
import { XMarkIcon } from '@heroicons/vue/24/outline'



const props = defineProps({
  categories: {type: Array },
  brands: {type: Array },
  filters: {type: Object},
  search: {type: Function},
  toggleModal: {type: Function},
  open: {type: Boolean}
})
</script>
