<script setup>
import { useCouponStore } from '@/stores/coupons'

const store = useCouponStore()

</script>

<template lang="pug">
p(class="mt-5 py-5 font-bold border-t border-gray-200") ¿Tienes un cupón?
div(class="flex")
  input(
    type="type"
    placeholder="Introduce un cupón"
    class="p-2 bg-white border-gray-300 w-full"
    v-model="store.couponInput"
  )

  button(
    type="button"
    class="p-3 bg-green-400 font-bold disabled:opacity-30"
    @click="store.applyCoupon"
    :disabled="store.isValidCoupon"
  ) Canjear

p(class="py-2 text-center text-sm font-extrabold") {{ store.couponValidationMessage }}
</template>