<template>
  <div class="p-8">
    <h1 class="text-4xl font-bold mx-3 mb-10">Ingredients</h1>
    <input type="text" class="rounded border-2 border-gray-200 w-full mx-3" placeholder="Search for Meals" v-model="keyword" @change="searchMeals" />
    <router-link
      :to="{ name: 'byIngredient', params: { ingredient: ingredient.strIngredient } }"
      v-for="ingredient of computedIngredients"
      :key="ingredient.idIngredient"
      class="block bg-white shadow rounded p-3 m-3"
    >
      <h3 class="text-2xl font-bold mb-2">{{ ingredient.strIngredient }}</h3>
      <p>{{ ingredient.strDescription }}</p>
    </router-link>
  </div>
</template>

<script setup>
import { onMounted, ref, computed } from "vue";
import axiosCLient from "../plugins/axios/axiosClient";

const ingrediets = ref([]);
const keyword = ref("");
const computedIngredients = computed(() => {
  if (!computedIngredients) {
    return ingrediets;
  }
  return ingrediets.value.filter(
    (i) => (i.strDescription || "").toLowerCase().includes(keyword.value.toLowerCase()) || i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase())
  );
});

onMounted(() => {
  axiosCLient.get("list.php?i=list").then(({ data }) => {
    ingrediets.value = data.meals;
  });
});
</script>

<style lang="scss" scoped></style>
