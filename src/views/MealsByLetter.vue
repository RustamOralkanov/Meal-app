<template>
  <div class="flex gap-2 justify-center py-5">
    <router-link :to="{ name: 'byLetter', params: { letter } }" v-for="letter of letters" :key="letter" class="text-2xl"> {{ letter }}</router-link>
  </div>
  <Meals :meals="meals" />
</template>

<script setup>
import { computed, onMounted, watch } from "vue";
import store from "../store";
import { useRoute } from "vue-router";
import Meals from "../components/Meals.vue";

const letters = "ABCDEFGHIKLMNOPQRSTVXYZ".split("");
const route = useRoute();
const meals = computed(() => store.state.mealsByLetter);

watch(route, () => {
  store.dispatch("searchMealsByLetter", route.params.letter);
});

onMounted(() => {
  store.dispatch("searchMealsByLetter", route.params.letter);
});
</script>
