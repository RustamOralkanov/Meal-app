<script setup>
import Navbar from "./components/Navbar.vue";
</script>

<template>
  <Navbar />
  <div class="bg-gray-100 h-full">
    <main>
      <router-view />
    </main>
  </div>
</template>

<style scoped></style>
