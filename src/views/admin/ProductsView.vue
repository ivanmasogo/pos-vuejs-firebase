<script setup>
import Link from '@/components/Link.vue'
import { useProductsStore } from '@/stores/products'
import Product from '@/components/Product.vue'


const products = useProductsStore()
</script>

<template lang="pug">
div.mt-10.mx-5
  Link(to="new-product") Nuevo Producto
  h1(class="text-4xl font-black my-10") Productos
  p(v-if="products.noResults") No hay resultados

  ul(
    v-else
    role="list"
    class="grid grid-cols-1 md:grid-cols-2 2xl:grid-cols-3 gap-5"
  )
    Product(
      v-for="product in products.productsCollection"
      :key="product.id"
      :product="product"
    )
</template>
