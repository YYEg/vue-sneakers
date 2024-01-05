<script setup>
defineProps({
  id: Number,
  title: String,
  imageUrl: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickFavorite: Function,
  onClickAdd: Function
})
</script>

<template>
  <div>
    <div
      class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer hover:-translate-y-2 hover:scale-105 hover:shadow-2xl transition h-full"
    >
      <img
        v-if="onClickFavorite"
        :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'"
        alt="Plus"
        class="absolute top-4 left-4"
        @click="onClickFavorite"
      />
      <img :src="imageUrl" alt="Sneakers" />
      <p class="mt-2 truncate line-clamp-1 text-base">{{ title }}</p>
      <div class="flex justify-between mt-5">
        <div class="flex flex-col">
          <span class="text-slate-500">Цена:</span>
          <b>{{ price }}</b>
        </div>
        <img
          v-if="onClickFavorite"
          :src="!isAdded ? '/plus.svg' : '/checked.svg'"
          alt="Plus"
          class="h-4/6"
          @click="onClickAdd"
        />
      </div>
    </div>
  </div>
</template>
