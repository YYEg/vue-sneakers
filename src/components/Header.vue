<template>
  <header class="flex justify-between items-center border-b border-slate-100 px-10 py-4">
    <div class="flex items-center gap-4">
      <img src="/logo.png" alt="Logo" class="w-10" />
      <div>
        <h2 class="text-xl font-bold uppercase">Vue sneakers</h2>
        <p class="text-slate-500">Все для хайпбиста</p>
      </div>
    </div>

    <ul class="flex items-center gap-10">
      <li class="flex items-center gap-3 text-slate-500 hover:text-black cursor-pointer">
        <img src="/cart.svg" alt="Cart" />
        <b>1337 руб.</b>
      </li>

      <li class="flex items-center gap-3 text-slate-500 hover:text-black cursor-pointer">
        <img src="/heart.svg" alt="Heart" />
        <span>Закладки</span>
      </li>

      <li class="flex items-center gap-3 text-slate-500 hover:text-black cursor-pointer">
        <img src="/profile.svg" alt="Heart" />
        <span>Профиль</span>
      </li>
    </ul>
  </header>
</template>
