<template>
    <div>
        <div class="p-8 pb-0">
            <input type="text" v-model="keyword" class="rounded border-2 border-gray-200 w-full"
                placeholder="Search for Meals" @change="searchMeals">
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
            <div v-for="meal of meals" :key="meal.idMeals" class="bg-white shadow rounded-xl">
                <router-link :to="{ name: 'mealDetails',params: {id: meal.idMeal}}">
                    <img :src="meal.strMealThumb" :alt="meal.strMeal" class="rounded-t-xl w-full h-48 object-cover">
                </router-link>
                <div class="p-3">
                <h3  class="font-bold">{{ meal.strMeal }}</h3>
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Beatae, reprehenderit?</p>
                <div class="flex items-center justify-between">
                <YoutubeButton :href ="meal.strYoutube"></YoutubeButton>    
                </div>
            </div>
            </div>
        </div>
    </div>
</template>
<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store/index.js";
import {useRoute} from "vue-router"
import YoutubeButton from "../components/YoutubeButton.vue";
const route = useRoute();
const keyword = ref('');
const meals = computed(() => store.state.searchMeals);
function searchMeals() {
    store.dispatch('searchMeals', keyword.value);

}
onMounted(()=>{
   keyword.value = route.params.name

   if (keyword.value) {
    searchMeals()
   }
})
</script>