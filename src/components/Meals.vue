<template>
  <div class="grid grid-cols-1 md:grid-cols-3 gap-3 p-8">
    <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal" />
  </div>
  <div v-if="!meals.length" class="flex justify-center p-10 text-4xl font-bold">There Are No Meals!</div>
</template>

<script setup>
import MealItem from "./MealItem.vue";

const { meals } = defineProps({
  meals: { type: Object, required: true },
});
</script>

<style lang="scss" scoped></style>
