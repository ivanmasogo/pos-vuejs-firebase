<template lang="pug">
div(class="flex justify-between p-1")
  dt(class="font-bold")
    slot(name="label")
  dd(class="text-gray-900")
    slot
</template>