<template>
  <div class="top">
    <FormIdol/>
  </div>
  <main class="top">
    <IdolList/>
  </main>
</template>

<script setup lang="ts">
import IdolList from './components/idols/IdolList.vue'
import FormIdol from './components/FormIdol.vue'
</script>

<style scoped>
.top {
  margin-top: 3rem;
}
</style>
