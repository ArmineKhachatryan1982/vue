<script setup>
import axios from 'axios';
import { onMounted, ref,reactive,provide, watch   } from 'vue';

import Header from './components/Header.vue' 
import CardList from './components/CardList.vue'  
import Drawer from './components/Drawer.vue' 
// ref mez misht veradarznum e objekt, dra hamar arjeqnery vercnelwuc dimum enq valuin

const items = ref([]) //{ value:[] }

const filters = reactive({
    sortBy:'title',
    searchQuery: '',
})

const onChangeSearchInput = (event)=>{
    
    filters.searchQuery = event.target.value
}

const onChangeSelect = (event) => {
    
   filters.sortBy = event.target.value
  
}
const fetchFavorites = async ()=>{

    try{
        
        const { data:favorites } = await  axios.get(`https://033b20b544163707.mokky.dev/favorites`)
        
        items.value = items.value.map(item =>{
            const favorite = favorites.find(favorite =>favorite.parentId === item.id )
            
            if(!favorite){
                return item;
            }
            return {
               ...item,
                isFavorite:true,
                favoriteId:favorite.id,
            };
        });
        
console.log(items.value)
    }catch(err){
        console.log(err)
    }



}
const addToFavorite =async(item)=>{
    item.isFavorite = true
}

const fetchItems =async () =>{

    try{
        const params = {
            sortBy:filters.sortBy,
           
        }
        if(filters.searchQuery){
            params.title = `*${filters.searchQuery}*`;
        }
      
        const { data } = await  axios.get(`https://033b20b544163707.mokky.dev/items`, {
            params
        })
        
        items.value = data.map((obj)=>({
            ...obj,
            isFavorite:false,
            isAdded:false
        }))
        console.log(items.value)

    }catch(err){
        console.log(err)
    }

}








onMounted( async () =>{

    await fetchItems();
    await fetchFavorites();
})
watch(filters,fetchItems)
provide('addToFavorite', addToFavorite);

// onMounted(async()=>{
//     // fetch('https://033b20b544163707.mokky.dev/items')
//     // .then((res)=>res.json())
//     // .then((data)=>{
//     //     console.log(data)
//     // })
//     // axios.get('https://033b20b544163707.mokky.dev/items').then((resp)=>console.log(resp.data))
//     try{
//         const { data } = await  axios.get('https://033b20b544163707.mokky.dev/items')
        
        
//         items.value = data
//         console.log(items.value)

//     }catch(err){
//         console.log(err)

//     }
// });
// kochvum e hooker watch
// watch(filters,async () => {
//     try{
//         console.log(7777)
//         const { data } = await  axios.get(
//             'https://033b20b544163707.mokky.dev/items?sortBy='+filters.sortBy)
        
        
//         items.value = data
//         console.log(items.value)

//     }catch(err){
//         console.log(err)

//     }

// });

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
                           @input="onChangeSearchInput"
                            class="border rounded-md py-2 pl-11 pr-4 outline-none focuse:border-gray-400"
                            type="text"
                            placeholder="Поиск"
                        />
                    </div>
                </div>
            </div>
            <CardList :items="items"  @addToFavorite="addToFavorite"/>
        </div>  
    </div>
    
</template>


<style scoped>

</style>
