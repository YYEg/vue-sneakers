<script setup>
import DrawerHead from './DrawerHead.vue'
import CartListItem from './CartListItem.vue'
import infoBlock from './infoBlock.vue'
import { ref, computed, inject } from 'vue'
import axios from 'axios'

const props = defineProps({
  totalPrice: Number,
  vatPrice: Number
})

const { cart } = inject('cart')

const cartIsEmpty = computed(() => {
  return cart.value.length === 0
})

const buttonDisabled = computed(() => isCreatingOrder.value || cartIsEmpty.value)

const isCreatingOrder = ref(false)
const createOrder = async () => {
  try {
    isCreatingOrder.value = true
    const { data } = await axios.post('https://c7191bbb87ac6c60.mokky.dev/orders', {
      items: cart.value,
      totalPrice: props.totalPrice.value
    })

    cart.value = []
    return data
  } catch (err) {
    console.log(err)
  } finally {
    isCreatingOrder.value = false
  }
}
</script>

<template>
  <div class="fixed top-0 left-0 w-full h-full bg-black z-10 opacity-70"></div>
  <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
    <DrawerHead />

    <div v-if="!totalPrice" class="flex h-full items-center justify-center">
      <infoBlock
        title="Корзина пуста"
        description="Добавьте хотя бы одну пару кроссовок, чтобы сделать заказ"
        image-url="/package-icon.png"
      />
    </div>

    <cart-list-item v-if="totalPrice" />
    <div v-if="totalPrice" class="flex flex-col gap-4 mb-6 mt-7">
      <div class="flex gap-2">
        <span>Итого:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>{{ totalPrice }} руб.</b>
      </div>

      <div class="flex gap-2">
        <span>Налог 5%:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>{{ vatPrice }} руб.</b>
      </div>

      <button
        :disabled="buttonDisabled"
        @click="createOrder"
        class="mt-4 w-full bg-lime-500 rounded-xl py-3 text-white disabled:bg-slate-300 hover:bg-lime-600 transition action:bg-lime-700 cursor-pointer"
      >
        Оформить заказ
      </button>
    </div>
  </div>
</template>
