<template>
  <div class="p-8">
    <input type="text" class="rounded border-2 border-gray-200 w-full" placeholder="Search for Meals" v-model="keyword" @change="searchMeals" />
  </div>
  <div class="grid grid-cols-1 md:grid-cols-3 gap-3 p-8">
    <div v-for="meal of meals" :key="meal.idMeal" class="bg-white shadow rounded-xl">
      <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }">
        <img :src="meal.strMealThumb" :alt="meal.strMeal" class="rounded-t-xl h-48 w-full object-cover" />
      </router-link>
      <div class="p-3">
        <h3 class="font-semibold">{{ meal.strMeal }}</h3>
        <p class="mb-4">Lorem ipsum dolor sit, amet consectetur adipisicing elit.</p>
        <div class="flex items-center justify-between">
          <YouTubeButton :href="meal.strYoutube">Youtbe</YouTubeButton>
          <router-link
            :to="{ name: 'mealDetails', params: { id: meal.idMeal } }"
            class="px-3 py-2 rounded border-2 border-orange-500 bg-orange-500 hover:bg-orange-600 hover:border-orange-600 text-white transition-colors"
            >View</router-link
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import store from "../store";
import { useRoute } from "vue-router";
import YouTubeButton from "../components/YouTubeButton.vue";

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
