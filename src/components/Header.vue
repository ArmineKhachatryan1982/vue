<template>
    <header class="flex justify-between border-b border-slate-300 px-10 py-8">
        <div class="flex items-center gap-4">
            <img src="/logo.png" alt="Logo" />
            <div>
                <h2 class="text-xl font-bold uppercase">Vue Sneakers</h2>
                <p class="text-slate-500">Магазин лучших кроццобок</p>
            </div>
        </div>
        <ul class="flex items-center gap-10">
            <li class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
                <img src="/cart.svg" alt="Cart" />
                <b>1205 руб. </b>
            </li>
            <li class="flex items-center cursor-pointer  gap-3 text-gray-500 hover:text-black">
                <img src="/heart.svg" alt="Cart" />
                <span>1205 руб. </span>
            </li>
            <li class="flex items-center cursor-pointer  gap-3 text-gray-500 hover:text-black">
                <img src="/profile.svg" alt="Cart" />
                <span>1205 руб. </span>
            </li>
        </ul>
    </header>
</template>