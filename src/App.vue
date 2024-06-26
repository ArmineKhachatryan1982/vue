<script setup>
import Header from './components/Header.vue' 
import Card from './components/Card.vue' 
import CardList from './components/CardList.vue'  
import Drawer from './components/Drawer.vue' 
const items=[{"id":1,"title":"Крассовки Feater reader","price":1200,"imageUrl":"/sneakers/sneakers-1.jpg"},{"id":2,"title":"Крассовки Broun  reader","price":1800,"imageUrl":"/sneakers/sneakers-2.jpg"},{"id":3,"title":"Крассовки Green  reader","price":2500,"imageUrl":"/sneakers/sneakers-3.jpg"},{"id":4,"title":"Крассовки Nike  reader","price":1900,"imageUrl":"/sneakers/sneakers-4.jpg"},{"id":5,"title":"Крассовки Puma  reader","price":2500,"imageUrl":"/sneakers/sneakers-5.jpg"},{"id":6,"title":"Крассовки Broun  reader","price":2400,"imageUrl":"/sneakers/sneakers-6.jpg"},{"id":7,"title":"Крассовки Broun1  reader","price":2500,"imageUrl":"/sneakers/sneakers-7.jpg"},{"id":8,"title":"Крассовки Broun2  reader","price":2800,"imageUrl":"/sneakers/sneakers-8.jpg"},{"id":9,"title":"Крассовки Broun3  reader","price":2800,"imageUrl":"/sneakers/sneakers-9.jpg"},{"id":10,"title":"Крассовки Broun4  reader","price":3500,"imageUrl":"/sneakers/sneakers-10.jpg"}] 

</script>

<template>
    <!-- <Drawer /> -->
    <div class="bg-white w-4/5 m-auto  rounded-xl shadow-xl mt-10">
        <Header />
       
        <div class="p-10">
            <div class=" border flex justify-between items-center">
                <h2 class="text-3xl font-bold m-auto mb-8" >Все кроссовки</h2>
                <div class="flex gap-4">
                    <select class="py-2 px-3 border rounded-md outline-none">
                        <option>По названи</option>
                        <option>По цене (дешеве)</option>
                        <option>По цене (дорогие)</option>
                    </select>
                
                    <div class="relative">
                        <img class="absolute left-4 top-3" src="/search.svg">
                        <input
                            class="border rounded-md py-2 pl-11 pr-4 outline-none focuse:border-gray-400"
                            type="text"
                            placeholder="Поиск"
                        />
                    </div>
                </div>
            </div>
            <CardList  />
        </div>  
    </div>
    
</template>


<style scoped>

</style>
