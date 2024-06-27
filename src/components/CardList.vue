<script setup>
import Card from './Card.vue'

defineProps({
  items:Array
})

const onClickAdd = ()=>{
  alert('added')
}

</script>

<template>
  
    <div class="border grid grid-cols-4 gap-5">
        <!-- <Card 
            title = "Мужские Крассовки Нике Блазер Мид"
            imageUrl = "/sneakers/sneakers-1.jpg"
            :price = "5000"
            :isFavorite = "false"
            :onClickAdd = "onClickAdd"
          
            :isAdded="true"
            /> -->
            <Card v-for="item in items"
              :key="item.id"
              :title = "item.title"
              :imageUrl = "item.imageUrl"
              :price = "item.price"
              :onClickAdd = "onClickAdd"
              :isFavorite = "false"
              
            />
        

    </div>

</template>
