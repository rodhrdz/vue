<template>
<div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-5 px-8">
      <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal" />
    
    </div>
        <div v-if="!meals.length" class="flex justify-center text-gray-600">
          There are not meals
        </div>
    </div>
</template>
<script setup>
import { computed, onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import store from "../store";
const meals = computed(() => store.state.mealsByIngredient);
const route = useRoute();


onMounted(() => {
    
    store.dispatch('searchMealsByIngredients', route.params.ingredient)
})
</script>