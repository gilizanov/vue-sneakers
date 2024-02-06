<template>
  <Cart
    v-if="cartIsOpen"
    :totalPrice="totalPrice"
    :vatPrice="vatPrice"
  />

  <div class="bg-white w-4/5 mx-auto rounded-xl shadow-xl mt-14 mb-14">
    <Header
      @open-cart="openCart"
      :total-price="totalPrice"
    />

    <div class="p-10">
      <router-view></router-view>
    </div>
  </div>
</template>

<script setup>
import { provide, ref, watch, computed } from 'vue'

import Cart from './components/Cart.vue'
import Header from './components/Header.vue'

/* Корзина (START)*/
const cart = ref([])
const cartIsOpen = ref(false)
const totalPrice = computed(() => cart.value.reduce((acc, item) => acc + item.price, 0))
const vatPrice = computed(() => Math.round((totalPrice.value * 5) / 100))

const closeCart = () => cartIsOpen.value = false
const openCart = () => cartIsOpen.value = true

const addToCart = (item) => {
  cart.value.push(item)
  item.isAdded = true
}

const removeFromCart = (item) => {
  cart.value.splice(cart.value.indexOf(item), 1)
  item.isAdded = false
}

watch(
  cart,
  () => {
    localStorage.setItem('cart', JSON.stringify(cart.value))
  },
  { deep: true }
)

provide('cart', {
  cart,
  closeCart,
  openCart,
  addToCart,
  removeFromCart
})
/* Корзина (END)*/
</script>

<style></style>
