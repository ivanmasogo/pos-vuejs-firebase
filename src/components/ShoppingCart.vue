<script setup>
import ShoppingCartItem from './ShoppingCartItem.vue'
import Amount from './Amount.vue'
import CouponForm from './CouponForm.vue'
import { useCartStore } from '@/stores/cart'
import { useCouponStore } from '@/stores/coupons'
import { formatCurrency } from '@/helpers/currency';

const cart = useCartStore()
const coupons = useCouponStore()
</script>

<template lang="pug">
p(
  v-if="cart.isEmpty"
  class="text-xl text-center text-gray-900"
) El carrito está vacío
div(v-else)
  p(class="text-4xl font-bold text-gray-900") Resumen de Venta 
  ul(
    role="list"
    class="mt-6 divide-y divide-gray-200"
  )
    ShoppingCartItem(
      v-for="item in cart.items"
      :key="item.id"
      :item="item"
    )
  dl(class="space-y-6 border-t border-gray-200 pt-6 text-sm font-medium text-gray-500")
    Amount
      template(#label) Subtotal:
      template(#default) {{formatCurrency(cart.subtotal)}}
    Amount
      template(#label) Impuestos:
      template(#default) {{formatCurrency(cart.taxes)}}
    Amount(v-if="coupons.isValidCoupon")
      template(#label) Descuento:
      template(#default) {{formatCurrency(coupons.discount)}}
    Amount
      template(#label) Total a pagar:
      template(#default) {{formatCurrency(cart.total)}}
  CouponForm

  button(
    type="button"
    class="mt-10 w-full bg-indigo-600 hover:bg-indigo-700 text-white uppercase font-bold p-3"
    @click="cart.checkout"
  ) Confirmar Compra
</template>