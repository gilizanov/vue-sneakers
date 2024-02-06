<template>
  <div v-auto-animate class="flex flex-col gap-4 mb-5 overflow-y-auto no-scrollbar">
    <CartItem
      v-for="item in cart"
      :key="item.id"
      :imageUrl="item.imageUrl"
      :title="item.title"
      :price="item.price"
      @on-click-remove="() => removeFromCart(item)"
    />
  </div>
</template>

<script setup>
import CartItem from './CartItem.vue'
import { inject } from 'vue'

const { cart, removeFromCart } = inject('cart')

</script>
