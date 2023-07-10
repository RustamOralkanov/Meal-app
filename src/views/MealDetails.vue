<template>
  <div class="w-[800px] mx-auto">
    <pre>{{ meal }}</pre>
    <h1 class="text-5xl font-bold mb-5">{{ meal.strMeal }}</h1>
    <img :src="meal.strMealThumb" :alt="meal.strMeal" />
    <div class="grid grid-cols-1 md:grid-cols-3 text-lg">
      <div><strong> Category:</strong> {{ meal.strCategory }}</div>
      <div><strong>Area:</strong> {{ meal.strArea }}</div>
      <div><strong>Tags:</strong> {{ meal.strTags }}</div>
    </div>
    <div class="grid grid-cols-1 md:grid-cols-2">
      <div>
        <h2 class="text-2xl font-semibold mb-3">Ingrediets</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)">
            <li v-if="meal[`strIngredient${ind + 1}`]">{{ ind + 1 }}. {{ meal[`strIngredient${ind + 1}`] }}</li>
          </template>
        </ul>
      </div>
      <div>
        <h2 class="text-2xl font-semibold mb-3">Measures</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)">
            <li v-if="meal[`strMeasure${ind + 1}`]">{{ ind + 1 }}. {{ meal[`strMeasure${ind + 1}`] }}</li>
          </template>
        </ul>
      </div>
    </div>
    <div class="mt-4">
      <YouTubeButton :href="meal.strYoutube">Go to Youtube</YouTubeButton>
      <a :href="meal.strSource" class="px-3 py-2 rounded border-2 border-orange-500 bg-orange-500 hover:bg-orange-600 hover:border-orange-600 text-white transition-colors"
        >View Original Source</a
      >
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axiosCLient from "../plugins/axios/axiosClient";
import YouTubeButton from "../components/YouTubeButton.vue";

const route = useRoute();
const meal = ref({});

onMounted(() => {
  axiosCLient.get(`lookup.php?i=${route.params.id}`).then(({ data }) => {
    meal.value = data.meals[0] || {};
  });
});
</script>

<style lang="scss" scoped></style>
