<script setup>
import DrawerHead from './DrawerHead.vue'
import CartListItem from './CartListItem.vue'
</script>

<template>
  <div class="fixed top-0 left-0 w-full h-full bg-black z-10 opacity-70"></div>
  <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
    <DrawerHead />
    <cart-list-item />
    <div class="flex flex-col gap-4 mb-6 mt-7">
      <div class="flex gap-2">
        <span>Итого:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>12999 руб.</b>
      </div>

      <div class="flex gap-2">
        <span>Налог 5%:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>900 руб.</b>
      </div>

      <button
        disabled=""
        class="mt-4 w-full bg-lime-500 rounded-xl py-3 text-white disabled:bg-slate-300 hover:bg-lime-600 transition action:bg-lime-700 cursor-pointer"
      >
        Оформить заказ
      </button>
    </div>
  </div>
</template>