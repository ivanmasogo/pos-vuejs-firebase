<script setup>
import { formatCurrency } from '@/helpers/currency'
import Amount from './Amount.vue'

defineProps({
  sale: {
    type: Object
  }
})


</script>

<template lang="pug">
div(class="border-t border-gray-200 space-y-6 py-6")
  h2(class="text-2xl font-black") Detalles Venta: 
  p(class="text-xl font-black text-gray-500") Productos Vendidos

  ul(
    role="list"
    class="mt-6 divide-y divide-gray-200 border-t border-gray-200 text-sm font-medium text-gray-500"
  )
    li(
      v-for="item in sale.items"
      class="flex space-x-6 py-6"
    )
      img(
        :src="item.image"
        :alt="'Imagen de ' + item.name"
        class="h-24 w-24 flex-none rounded-lg"
      )

      div(
        class="flex-auto space-y-2"
      )
        h3(class="text-gray-900") {{ item.name }}
        p {{ formatCurrency(item.price) }}
        p Cantidad: {{ item.quantity }}

  dl(class="space-y-6 border-t border-gray-200 pt-6 text-sm font-medium text-gray-500")
    Amount
      template(#label) Subtotal:
      template(#default) {{formatCurrency(sale.subtotal)}}
    Amount
      template(#label) Impuestos:
      template(#default) {{formatCurrency(sale.taxes)}}
    Amount(v-if="sale.discount" class="bg-green-200 p-2")
      template(#label) Descuento:
      template(#default) {{formatCurrency(sale.discount)}}
    Amount
      template(#label) Total a pagar:
      template(#default) {{formatCurrency(sale.total)}}
</template>
