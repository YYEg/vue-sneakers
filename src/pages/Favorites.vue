<script setup>
import { onMounted, ref, inject } from 'vue'
import axios from 'axios'

import CardList from '../components/CardList.vue'

const favorites = ref([])
const { cart } = inject('cart')

onMounted(async () => {
  try {
    const { data } = await axios.get(
      'https://c7191bbb87ac6c60.mokky.dev/favorites?_relations=items'
    )
    console.log(data)

    favorites.value = data.map((obj) => obj.item)
  } catch (err) {
    console.log(err)
  }

  const localCart = localStorage.getItem('cart')

  if (localCart) {
    cart.value = JSON.parse(localCart)
  } else {
    cart.value = []
  }
})
</script>

<template>
  <h2 class="text-3xl font-bold mb-8">Мои избранные</h2>
  <CardList :items="favorites" :isFavorites="true" />
</template>
