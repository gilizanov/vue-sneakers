<template>
  <div class="flex justify-between items-center mb-8">
    <h2 class="text-3xl font-bold">Мои закладки</h2>
  </div>
  <CardList :items="favorites" is-favorites />
</template>

<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import CardList from '@/components/CardList.vue';

const favorites = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get('https://97cabdd60b79c72d.mokky.dev/favorites?_relations=items')
    favorites.value = data.map(obj => obj.item)
  } catch (err) {
    console.log(err)
  }
})
</script>
