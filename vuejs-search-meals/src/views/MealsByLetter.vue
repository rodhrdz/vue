<template>
    <div>
        <div class="flex flex-col p-8 ">
            <input type="text" class="rounded border-2 border-gray-200 w-full" placeholder="Search for Meals">
            <div class="flex justify-center gap-2 mt-2">
                <router-link :to="{ name: 'byLetter', params: { letter } }" 
                v-for="letter of letters" 
                :key="letter">
                    {{ letter }}
                </router-link>
            </div>
        </div>
    

    <div>
       <pre>{{ meals }}</pre>
    </div>
</div>
</template>
<script setup>
import { computed, onMounted } from "vue";
import { useRoute } from "vue-router";
import store from '../store'
const route = useRoute();
const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split("");
const meals = computed(() => store.state.mealsByLetter)
onMounted(()=>{
    store.dispatch('searchMealsByLetter',route.params.letter)

})
</script>