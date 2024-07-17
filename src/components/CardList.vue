<script setup>
// import {inject} from 'vue'
import Card from './Card.vue'


// const addToFavorite = inject('addToFavorite')

// const onClickFavorite = ()=>{
//     alert()
//     const obj = {
//         ...props,
//         parentId:props.id,

//     };
//     addToFavorite(obj)
// }

defineProps({
  items:Array
})
// injecti poxaren ogtagorcenq emit
const emit = defineEmits(['addToFavorite','addToCart']);

// const onClickAdd = ()=>{
//   // alert('added')
//   emit('addToFavorite',)
// }


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
              :id="item.id"
              :key="item.id"
              :title = "item.title"
              :imageUrl = "item.imageUrl"
              :price = "item.price"
           
              :onClickFavorite = "()=>emit('addToFavorite',item)" 
              :onClickAdd = "()=>emit('addToCart',item)"
              :isFavorite = "item.isFavorite"
           
              
            />
        

    </div>

</template>
