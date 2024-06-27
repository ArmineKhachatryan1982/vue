<script setup>
import axios from 'axios';
import { onMounted, ref, watch  } from 'vue';

import Header from './components/Header.vue' 
import Card from './components/Card.vue' 
import CardList from './components/CardList.vue'  
import Drawer from './components/Drawer.vue' 
// ref mez misht veradarznum e objekt, dra hamar arjeqnery vercnelwuc dimum enq valuin

const items = ref([]) //{ value:[] }
const sortBy = ref('');
const searchQuery = ref('');
const onChangeSelect = (event) => {
    sortBy.value=event.target.value
}

onMounted(async()=>{
    // fetch('https://033b20b544163707.mokky.dev/items')
    // .then((res)=>res.json())
    // .then((data)=>{
    //     console.log(data)
    // })
    // axios.get('https://033b20b544163707.mokky.dev/items').then((resp)=>console.log(resp.data))
    try{
        const { data } = await  axios.get('https://033b20b544163707.mokky.dev/items')
        
        
        items.value = data
        console.log(items.value)

    }catch(err){
        console.log(err)

    }
});
// kochvum e hooker watch
watch(sortBy,async () => {
    try{
        const { data } = await  axios.get('https://033b20b544163707.mokky.dev/items?sortBy='+sortBy.value)
        
        
        items.value = data
        console.log(items.value)

    }catch(err){
        console.log(err)

    }

});

</script>

<template>
    <!-- <Drawer /> -->
    <div class="bg-white w-4/5 m-auto  rounded-xl shadow-xl mt-10">
        <Header />
       
        <div class="p-10">
            <div class=" border flex justify-between items-center">
                <h2 class="text-3xl font-bold m-auto mb-8" >Все кроссовки</h2>
                <div class="flex gap-4">
                    <select  @change="onChangeSelect" class="py-2 px-3 border rounded-md outline-none">
                        <option value="name">По названи</option>
                        <option value="price">По цене (дешеве)</option>
                        <option value="-price">По цене (дорогие)</option>
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
            <CardList :items="items" />
        </div>  
    </div>
    
</template>


<style scoped>

</style>
