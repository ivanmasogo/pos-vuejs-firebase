<script setup>
import { RouterLink } from 'vue-router'

defineProps({
  to: {
    type: String
  }
});

</script>

<template lang="pug">
RouterLink(
  class="rounded bg-green-400 hover:bg-green-500 font-bold py-1 px-3 lg:py-2 lg:px-10"
  :to="{name: to}"  
)
  slot
</template>

<style scoped>

</style>