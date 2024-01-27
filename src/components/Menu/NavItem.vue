<script setup lang="ts">
import { RouterLink } from 'vue-router';
const props = defineProps<{
  path: string
  name: string
}>()
</script>
<template>
    <RouterLink :to="props.path">{{ name }}</RouterLink>
</template>

<style scoped>
a.router-link-exact-active {
  color: var(--color-text);
}

a.router-link-exact-active:hover {
  background-color: transparent;
}

a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

a:first-of-type {
  border: 0;
}
</style>