<script setup>
import { useSalesStore } from '@/stores/sales'
import { ref } from 'vue'
import VueTailwindDatePicker from 'vue-tailwind-datepicker'
import SaleDetails from '@/components/SaleDetails.vue'
import { formatCurrency } from '@/helpers/currency'

const sales = useSalesStore()

const formatter = ref({
  date: 'DD/MM/YYYY',
  month: 'MMMM'
})
</script>

<template lang="pug">
div
  h1(class="text-4xl font-black my-10") Resumen de Ventas
  div(class="md:flex md:items-start gap-5 ")
    div(class="md:w-1/2 lg:w-1/3 flex justify-center p-5 bg-transparent")
      VueTailwindDatePicker(
        i18n="es"
        as-single
        no-input
        v-model="sales.date"
        :formatter="formatter"
      )
    div(class="md:w-1/2 lg:w-2/3 space-y-5 lg:h-screen lg:overflow-y-scroll p-5 pb-32")
      p(
        v-if="sales.isDateSelected"
        class="text-center text-lg"
      ) Ventas de la fecha: 
        span(class="font-black") {{ sales.date }} 

      p(
        v-else
        class="text-center text-lg"
      ) Selecciona una fecha

      div(
        v-if="sales.salesCollection.length"
        class="space-y-5"
      )
        p(class="text-right text-2xl") Total del día: 
          span(class="font-black") {{ formatCurrency(sales.totalSalesOfDay) }}
        SaleDetails(
          v-for="sale in sales.salesCollection"
          :key="sale.id"
          :sale="sale"
        )

      p(v-else-if="sales.noSales" class="text-lg text-center") No hay ventas en este día
</template>
