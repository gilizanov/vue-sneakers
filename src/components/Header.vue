<template>
    <header class="flex justify-between items-center border-b border-slate-300 px-10 py-8">
    <router-link to="/">
      <div class="flex items-center gap-4">
        <img src="/logo.png" class="w-10" alt="Лого">
        <div>
          <h1 class="text-xl font-bold uppercase">Vue Sneakers</h1>
          <p class="text-slate-500">Магазин лучших кроссовок</p>
        </div>
      </div>
    </router-link>
    <nav>
      <ul class="flex items-center gap-3">
        <li>
          <button @click="() => emit('openCart')" class="flex items-center gap-3">
            <img src="/cart.svg" alt="Корзина">
            <span class="font-bold text-gray-600 hover:text-black">{{ totalPrice }} руб.</span>
          </button>
        </li>
        <li>
          <button class="flex items-center gap-3">
            <img src="/heart.svg" alt="Закладки">
            <span class="text-gray-500 hover:text-black"><router-link to="/favorites">Закладки</router-link></span>
          </button>
        </li>
        <li>
          <button class="flex items-center gap-3">
            <img src="/profile.svg" alt="Профиль">
            <span class="text-gray-500 hover:text-black">Профиль</span>
          </button>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script setup>
  const emit = defineEmits(['openCart'])
  defineProps({
    totalPrice: Number
  })
</script>
