<script setup>
const emit = defineEmits(['openDrawer'])

defineProps({
  totalPrice: Number
})
</script>

<template>
  <header class="flex justify-between items-center border-b border-slate-100 px-10 py-4">
    <router-link to="/" class="flex items-center gap-4">
      <img src="/logo.png" alt="Logo" class="w-10" />
      <div>
        <h2 class="text-xl font-bold uppercase">Vue sneakers</h2>
        <p class="text-slate-500">Все для хайпбиста</p>
      </div>
    </router-link>

    <ul class="flex items-center gap-10">
      <li
        @click="emit('openDrawer')"
        class="flex items-center gap-3 text-slate-500 hover:text-black cursor-pointer"
      >
        <img src="/cart.svg" alt="Cart" />
        <b>{{ totalPrice }} руб.</b>
      </li>

      <router-link to="/favorites">
        <li class="flex items-center gap-3 text-slate-500 hover:text-black cursor-pointer">
          <img src="/heart.svg" alt="Heart" />
          <span>Избранное</span>
        </li>
      </router-link>

      <li class="flex items-center gap-3 text-slate-500 hover:text-black cursor-pointer">
        <img src="/profile.svg" alt="Heart" />
        <span>Профиль</span>
      </li>
    </ul>
  </header>
</template>
