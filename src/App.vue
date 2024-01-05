<script setup>
import { ref, watch, provide, computed } from 'vue'
import axios from 'axios'

import Header from './components/Header.vue'

import Drawer from './components/Drawer.vue'

/*Корзина*/
const cart = ref([])
const isCreatingOrder = ref(false)

const drawerOpen = ref(false)
const closeDrawer = () => {
  drawerOpen.value = false
}

const openDrawer = () => {
  drawerOpen.value = true
}

const addToCart = (item) => {
  cart.value.push(item)
  item.isAdded = true
}

const removeFromCart = (item) => {
  cart.value.splice(cart.value.indexOf(item), 1)
  console.log(cart.value)
  item.isAdded = false
}

const createOrder = async () => {
  try {
    isCreatingOrder.value = true
    const { data } = await axios.post('https://c7191bbb87ac6c60.mokky.dev/orders', {
      items: cart.value,
      totalPrice: totalPrice.value
    })

    cart.value = []
    return data
  } catch (err) {
    console.log(err)
  } finally {
    isCreatingOrder.value = false
  }
}

const totalPrice = computed(() => {
  return cart.value.reduce((acc, item) => {
    return acc + item.price
  }, 0)
})

const cartIsEmpty = computed(() => {
  return cart.value.length === 0
})

const cartButtonDisabled = computed(() => isCreatingOrder.value || cartIsEmpty.value)



watch(
  cart,
  () => {
    localStorage.setItem('cart', JSON.stringify(cart.value))
  },
  {
    deep: true
  }
)

provide('cart', {
  cart,
  closeDrawer,
  openDrawer,
  addToCart,
  removeFromCart
})
</script>

<template>
  <Drawer
    v-if="drawerOpen"
    :totalPrice="totalPrice"
    :vatPrice="totalPrice * 0.05"
    @create-order="createOrder"
    :button-disabled="cartButtonDisabled"
  />

  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-14">
    <Header :totalPrice="totalPrice" @open-drawer="openDrawer" />

    <div class="p-10">
      <router-view></router-view>
    </div>
  </div>
</template>
