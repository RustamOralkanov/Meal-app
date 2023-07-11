<template>
  <header class="bg-white shadow-md h-16 flex justify-between items-center">
    <router-link :to="{ name: 'home' }" class="px-5"> Home </router-link>
    <div class="flex items-center gap-1 h-full">
      <router-link :to="{ name: 'byName' }" class="px-2 h-full hover:bg-purple-200 inline-flex items-center transition-colors"> Search Meals </router-link>
      <router-link :to="{ name: 'byLetter' }" class="px-2 h-full hover:bg-purple-200 inline-flex items-center transition-colors"> Meals by Letter </router-link>
      <router-link :to="{ name: 'ingredients' }" class="px-2 h-full hover:bg-purple-200 inline-flex items-center transition-colors"> Meals by Ingrediets </router-link>
    </div>
  </header>
</template>

<script setup></script>

<style lang="scss" scoped></style>
