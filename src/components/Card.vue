<template>
  <li>
    <article
      class="bg-white flex flex-col h-full relative border border-slate-200 rounded-3xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition"
    >
      <button v-if="onClickFavorite" @click="onClickFavorite" class="absolute top-7 left-7">
        <img :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'" alt="Добавить в избранное" />
      </button>
      <div>
        <img :src="imageUrl" alt="Кроссовки" />
      </div>
      <p class="mt-auto">{{ title }}</p>
      <div class="flex items-center justify-between mt-5">
        <div>
          <div class="text-slate-400 uppercase">Цена:</div>
          <div>{{ price }} руб.</div>
        </div>
        <button v-if="onClickAdd" @click="onClickAdd">
          <img :src="!isAdded ? '/plus.svg' : '/checked.svg'" alt="Добавить" />
        </button>
      </div>
    </article>
  </li>
</template>

<script setup>
defineProps({
  id: Number,
  imageUrl: String,
  title: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickFavorite: Function,
  onClickAdd: Function
})

</script>
