<template>
  <div class="p-8">
    <input type="text" class="rounded border-2 border-gray-200 w-full" placeholder="Search for Meals" v-model="keyword" @change="searchMeals" />
  </div>
  <div class="grid grid-cols-1 md:grid-cols-3 gap-3 p-8">
    <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal" />
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import store from "../store";
import { useRoute } from "vue-router";
import MealItem from "../components/MealItem.vue";

const route = useRoute();
const keyword = ref("");
const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
  store.dispatch("searchMeals", keyword.value);
}

onMounted(() => {
  keyword.value = route.params.name;
  if (keyword.value) {
    searchMeals();
  }
});
</script>
