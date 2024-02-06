<template>
  <div class="relative flex items-center w-full border border-slate-200 p-4 rounded-xl gap-2">
    <img class="w-16 h-16" :src="imageUrl" :alt="title" />

    <div class="w-8/12">
      <p>{{ title }}</p>
      <div class="font-bold">{{ price }} руб.</div>
    </div>

    <button @click="emit('onClickRemove')" class="absolute right-2 top-2">
      <img class="opacity-60 hover:opacity-100 cursor-pointer transition" src="/close.svg" alt="Закрыть"/>
    </button>
  </div>
</template>

<script setup>
const emit = defineEmits(['onClickRemove'])

defineProps({
  id: Number,
  imageUrl: String,
  title: String,
  price: Number
})
</script>
