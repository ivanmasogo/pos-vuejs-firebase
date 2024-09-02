<script setup>
import { RouterLink } from 'vue-router'
import Link from './Link.vue'
import Logo from './Logo.vue'

</script>

<template lang="pug">
header(class="px-10 py-5 bg-gray-700 flex flex-col lg:flex-row justify-between gap-3 absolute top-0 w-full z-10") 
  div
    Logo
  nav(class="flex flex-row justify-between items-center")
    RouterLink(:to="{name: 'products'}" class="rounded text-white font-bold lg:p-2") Productos
    RouterLink(:to="{name: 'sales'}" class="rounded text-white font-bold lg:p-2") Ventas
    Link(to="shop") Ir a tienda

</template>
