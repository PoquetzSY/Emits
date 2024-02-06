<template>
  <div class="top">
    <h1>Registrar nuevo Idol</h1>
    <FormIdol @add-Idol="addIdol"/>
  </div>
  <main class="top">
    <IdolList :idols="idols"/>
  </main>
</template>

<script setup lang="ts">
import IdolList from './components/idols/IdolList.vue'
import FormIdol from './components/FormIdol.vue'
import Idols from './data/IdolData'
import type { IIDolInfo } from './interfaces/IIdolInfo'
import { ref } from 'vue'

const idols = ref(Idols);

function addIdol(idol: IIDolInfo) {
    idols.value.push(idol);
}
console.log(idols);

</script>

<style scoped>
.top {
  margin-top: 3rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
