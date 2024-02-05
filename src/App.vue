<script setup lang="ts">
import IdolList from './components/idols/IdolList.vue'
</script>

<template>
  <div class="top">
    <h1>Vue 3</h1>
    <p>Vue 3 is the latest version of Vue.js. It is a progressive framework for building user interfaces. It is designed from the ground up to be incrementally adoptable.</p>
  </div>
  <main class="top">
    <IdolList/>
  </main>
</template>

<style scoped>
.top {
  margin-top: 3rem;
}
</style>
