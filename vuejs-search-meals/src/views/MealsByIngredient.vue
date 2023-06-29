<template>
<Meals :meals="meals"></Meals>
</template>
<script setup>
import { computed, onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import store from "../store";
import Meals from "../components/Meals.vue";
const meals = computed(() => store.state.mealsByIngredient);
const route = useRoute();


onMounted(() => {
    
    store.dispatch('searchMealsByIngredient', route.params.ingredient)
})
</script>