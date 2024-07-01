<script setup>
import {inject} from 'vue'

defineProps({
    id:Number,
    title: String,
    imageUrl: String,
    price: Number,
    isFavorite:Boolean,
    isAdded:Boolean,
    onClickFavorite:Function,
   
})
const addToFavorite = inject('addToFavorite')
const onClickFavorite = ()=>{
    const obj={
        parentId:id,

    };
}


</script>
   <template>
        <div class="relative m-10 border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl">
            
            <img 
               :src = "!isFavorite ? '/like-1.svg' : '/like-2.svg'" 
                alt = "Like 1" 
                class = "absolute top-0 left-0"
                @click="onClickFavorite"
                 />
            <img :src="imageUrl" alt ="Sneaker"/>
            <p class = "mt-2"> {{ title }}</p>
        
            <div class="flex justify-between mt-5">
                <div class="flex flex-col">
                        <span class="text-slate-400">Цена:</span>
                        <b>{{ price }} руб.</b>
                </div>
                <img @click="onClickAdd" :src="!isAdded ? '/plus.svg' : '/checked.svg'" alt="Plus" />
            </div>
        </div>
</template>
