<script setup lang="ts">

import { ref } from 'vue';

const name = ref('Luis');
const error = ref(false);
const hidden = ref(true);
const Namevalidation = () => {
  if (name.value.length < 1) {
    error.value = true;

  } else {
    error.value = false;
  }
}

</script>
<template>
  <div class="about">
    <h1>This is an home page</h1>
    <h2>My name is:</h2>
    <p v-if="error">Please, enter a character</p>
    <input @input="Namevalidation()" type="text" v-model="name">
    <p>Your name is: {{ name }}</p>
  </div>
</template>

<style scoped>
.about {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.error {
  color: red;
}

@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
