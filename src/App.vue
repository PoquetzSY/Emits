<template>
  <div class="top">
    <h1>Registrar nuevo Idol</h1>
    <FormIdol/>
  </div>
  <main class="top">
    <IdolList />
  </main>
</template>

<script setup lang="ts">
import IdolList from './components/idols/IdolList.vue'
import FormIdol from './components/FormIdol.vue'

</script>

<style scoped>
.top {
  margin-top: 3rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
