<template>
  <div class="flex flex-col items-center text-center">
    <img width="120" height="120" :src="imageUrl" alt="Cart info" />
    <h2 class="mt-4 text-2xl font-medium">{{ title }}</h2>
    <p class="text-gray-400">{{ descr }}</p>
  </div>
</template>

<script setup>
defineProps({
  imageUrl: String,
  title: String,
  descr: String
})
</script>
