<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>
  <div class="flex flex-col fixed top-0 right-0 bg-white w-96 h-full z-20 p-8">

    <CartHead />

    <div v-if="!totalPrice || orderId" class="my-auto">
      <EmptyCart
      v-if="!totalPrice && !orderId"
      title="Корзина пустая"
      descr="Добавьте хотя бы одну пару кроссовок, чтобы сделать заказ"
      imageUrl="/package-icon.png"
    />

    <EmptyCart
      v-if="orderId"
      title="Заказ оформлен!"
      :descr="`Ваш заказ #${orderId} скоро будет передан в службу доставки`"
      imageUrl="/order-success-icon.png"
    />
    </div>

    <div v-else class="flex flex-col h-full">
    <CartList />

    <div class="flex flex-col gap-4 mt-auto">
      <div class="flex hustify-between gap-2">
        <span>Итого:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <div class="font-bold">{{ totalPrice }} руб.</div>
      </div>
      <div class="flex hustify-between gap-2">
        <span>Налог:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <div class="font-bold">{{ vatPrice }} руб.</div>
      </div>
      <button
        :disabled="btnDisabled"
        class="bg-lime-500 w-full rounded-xl py-3 text-white disabled:bg-slate-300 disabled:cursor-default cursor-pointer hover:bg-lime-600 transition active:bg-lime-700"
        @click="createOrder"
      >
      Оформить заказ
    </button>
    </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, inject } from 'vue'
import axios from 'axios'

import CartHead from './CartHead.vue'
import CartList from './CartList.vue'
import EmptyCart from './EmptyCart.vue'

const isCreating = ref(false)
const orderId = ref(null)

const { cart } = inject('cart')
const props = defineProps({
  totalPrice: Number,
  vatPrice: Number,
  buttonDisabled: Boolean
})

const createOrder = async () => {
  try {
    isCreating.value = true
    const { data } = await axios.post(`https://97cabdd60b79c72d.mokky.dev/orders`, {
      items: cart.value,
      totalPrice: props.totalPrice.value,
    })

    cart.value = []

    orderId.value = data.id
  } catch (err) {
    console.log(err)
  } finally {
    isCreating.value = false
  }
}

const cartIsEmpty = computed(() => cart.value.length === 0)
const btnDisabled = computed(() => isCreating.value || cartIsEmpty.value)

</script>

