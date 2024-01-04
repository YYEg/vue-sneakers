<script setup>
const emit = defineEmits(['onClickRemove'])

defineProps({
  id: Number,
  title: String,
  imageUrl: String,
  price: Number
})
</script>

<template>
  <div class="flex items-center border border-slate-200 rounded-xl p-4 gap-4">
    <img :src="imageUrl" :alt="title" class="w-16 h-16" />
    <div class="flex flex-col flex-1">
      <p>{{ title }}</p>

      <div class="flex justify-between mt-2">
        <b class="flex-1">{{ price }} руб.</b>
        <img
          @click="emit('onClickRemove')"
          src="/close.svg"
          alt="Close"
          class="opacity-40 hover:opacity-100 cursor-pointer transition hover:rotate-45"
        />
      </div>
    </div>
  </div>
</template>
