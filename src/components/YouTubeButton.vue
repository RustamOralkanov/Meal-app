<template>
  <a :href="href" target="_blank" class="px-3 py-2 rounded border-2 border-red-500 bg-red-500 hover:bg-red-600 hover:border-red-600 text-white transition-colors">
    <slot>YouTube</slot>
  </a>
</template>

<script setup>
const props = defineProps({
  href: {
    type: String,
  },
});
</script>

<style lang="scss" scoped></style>
