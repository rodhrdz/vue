<template>
    <div>
        <div class="flex flex-col p-8 ">
            <input type="text" class="rounded border-2 border-gray-200 w-full" placeholder="Search for Meals">
            <div class="flex justify-center gap-2 mt-2">
                <router-link :to="{ name: 'byLetter', params: { letter } }" v-for="letter of letters" :key="letter">
                    <h1
                     class="text-3xl transition-colors text-orange-400 font-bold hover:bg-orange-100 hover:text-black">
                        {{ letter }}
                    </h1>
                    
                </router-link>
            </div>
        </div>
        <Meals :meals="meals"></Meals>
    </div>
</template>
<script setup>
import { computed, onMounted, watch } from "vue";
import { useRoute } from "vue-router";
import store from '../store'
import Meals from "../components/Meals.vue";

const route = useRoute();
const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split("");
const meals = computed(() => store.state.mealsByLetter)

watch(route, () => {
    store.dispatch('searchMealsByLetter', route.params.letter)

})

onMounted(() => {
    store.dispatch('searchMealsByLetter', route.params.letter)

})
</script>