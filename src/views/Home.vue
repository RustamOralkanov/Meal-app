<template>
  <div class="flex p-8 flex-col items-center">
    <input type="text" class="rounded border-2 border-gray-200 w-full" placeholder="Search for Meals" />
    <div class="flex gap-1">
      <router-link :to="{ name: 'byLetter', params: { letter } }" v-for="letter of letters"> {{ letter }}</router-link>
    </div>
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import axiosCLient from "../plugins/axios/axiosClient";

const meals = computed(() => store.state.meals);
const ingrediets = ref([]);

const letters = "ABCDEFGHIKLMNOPQRSTVXYZ".split("");

onMounted(async () => {
  const response = await axiosCLient.get("list.php?i=list");
  ingrediets.value = response.data;
  console.log(response.data);
});
</script>
