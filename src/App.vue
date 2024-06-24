<script setup>
import Header from './components/Header.vue' 

import CardList from './components/CardList.vue'  


</script>

<template>
    <div class="bg-white w-4/5 m-auto  rounded-xl shadow-xl mt-10">
        <Header />
        <!-- <div class="p-10">
            <h2 class="text-3xl font-bold m-auto mb-10" >Все кроссовки</h2>
            <CardList />
            
        </div> -->
        <div>
            <div class="relative m-10 border-slate-100 rounded-3xl p-8 cursor-pointer">
                <img src="\like-2.svg" alt="Like 1" 
                class="absolute top-0 left-0"/>
                <img src="\sneakers\sneakers-1.jpg" alt ="Sneaker"/>
                <p> mans clouth</p>
            </div>
            <div class="flex justify-between">
                <div class="flex flex-col">
                        <span class="text-slate-400">Цена:</span>
                        <b>2500 руб.</b>
                </div>
                <img  :src="!isAdded ? '/plus.svg' : '/checked.svg'" alt="Plus" />
            </div>

        </div>
        
    </div>
    
</template>


<style scoped>

</style>
