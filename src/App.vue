<script setup>
import axios from 'axios';
import { onMounted, ref,reactive,provide, watch,   } from 'vue';

import Header from './components/Header.vue' 
import CardList from './components/CardList.vue'  
import Drawer from './components/Drawer.vue' 
// ref mez misht veradarznum e objekt, dra hamar arjeqnery vercnelwuc dimum enq valuin

const items = ref([]) //{ value:[] }
const cart = ref([]) //define array


const drawerOpen = ref(false)
const closeDrawer = () =>{

    drawerOpen.value = false
}
const openDrawer = () =>{
    
    drawerOpen.value = true
}

const filters = reactive({
    sortBy:'title',
    searchQuery: '',
})

const onChangeSearchInput = (event)=>{
    
    filters.searchQuery = event.target.value
}
const addToCart =(item)=>{
    cart.value.push(item);
    console.log("aaa")
    console.log|(item)

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
//Card.vue-i megic  onClickFavorite click favorite aneluc  kanchum enq addToFavorite function 
const addToFavorite = async(item) => {
  
    try{
     

        if(!item.isFavorite){
           
                const obj = {
                 parentId:item.id
              }
              item.isFavorite = true
         
            const { data } = await  axios.post(`https://033b20b544163707.mokky.dev/favorites`,obj)
           
            item.favoriteId = data.id;
            console.log(data)

        }else{
            // alert(444);
            item.isFavorite = false;
            await  axios.delete(`https://033b20b544163707.mokky.dev/favorites/${item.favoriteId}`)
            item.favoriteId = null;
        }
       

    }catch (err) {

        console.log(err)

    }
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
        // cikl enq frum data-i vra  ev tvjalnery pahum enq tvjal formatov avelacnum enq naxnakan  isFavorite:false,isAdded:false
        items.value = data.map((obj)=>({
            ...obj,
            isFavorite:false,
            favoriteId:null,
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
provide('cartActions', {
    closeDrawer,
    openDrawer
});

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
 <Drawer v-if = "drawerOpen"/>
    <div class="bg-white w-4/5 m-auto  rounded-xl shadow-xl mt-10">
        <Header @open-drawer="openDrawer" />
       
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
            <CardList :items="items"  @add-to-favorite="addToFavorite" @add-to-cart="addToCart"/>
        </div>  
    </div>
    
</template>


<style scoped>

</style>
