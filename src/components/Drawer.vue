<script setup>
import DrawerHead from './DrawerHead.vue'
import CartItemList from './CartItemList.vue'


</script>
<template>
    <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>
    <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8">
        <DrawerHead/>
        <CartItemList/>
        <div class="flex flex-col gap-4 my-7">
            <div class="flex gap-2">
                <span>Итого:</span>
                <div class="flex-1 border-b border-dashed"></div>
                <b>12990 Q</b>
            </div> 
            <div class="flex gap-2">
                <span>Налог 5%:</span>
                <div class="flex-1 border-b border-dashed"></div>
                <b>900 Q</b>
            </div>  
        <button disabled="" class="disabled:bg-slate-300 transition bg-lime-500 w-full rounded-xl py-3  text-white hover:bg-lime-600 active:bg-lime-700 cursor-pointer">
            Оформитъ заказ
        </button>   
        </div>
        
    </div>
   
</template>