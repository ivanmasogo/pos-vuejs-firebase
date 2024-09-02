<script setup>
import { useProductsStore } from '@/stores/products';
import Link from './Link.vue'
import Logo from './Logo.vue'

const products = useProductsStore()
</script>

<template lang="pug">
header(class="px-10 py-5 bg-gray-700 flex flex-col lg:flex-row gap-5 lg:items-center lg:justify-between absolute top-0 w-full z-10") 
  div
    Logo
    div(class="flex gap-5 text-white")
      h2(class="text-lg font-extrabold hidden lg:block") Filtros: 
      div(
        class="flex items-center gap-2 mt-2 lg:mt-0"
        v-for="category in products.categories"
        :key="category.id"
      )
        input(
          type="radio" 
          name="category" 
          :value="category.id" 
          class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500"
          :checked="products.selectedCategory === category.id"
          @change="products.selectedCategory = +$event.target.value"
          )
        label(class="text-gray-100") {{ category.name }}
      
  nav
    Link(to="sales") Administrar

</template>
