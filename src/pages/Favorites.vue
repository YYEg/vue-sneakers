<script setup>

import { onMounted, ref } from "vue";
import axios from "axios";

const favorites = ref([])

onMounted(async () => {
    try {
        const {data} = await axios.get('https://c7191bbb87ac6c60.mokky.dev/favorites')
          
    } catch (err) {
        console.log(err)
    }
})
</script>

<template>
    <h1>Favorites</h1>
</template>