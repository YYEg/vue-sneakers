<script setup>
import { ref, watch, provide, computed } from 'vue'

import Header from './components/Header.vue'

import Drawer from './components/Drawer.vue'

/*Корзина*/
const cart = ref([])

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

const totalPrice = computed(() => {
  return cart.value.reduce((acc, item) => {
    return acc + item.price
  }, 0)
})

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
  <Drawer v-if="drawerOpen" :totalPrice="totalPrice" :vatPrice="totalPrice * 0.05" />

  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl mt-14">
    <Header :totalPrice="totalPrice" @open-drawer="openDrawer" />

    <div class="p-10">
      <router-view></router-view>
    </div>
  </div>
</template>
