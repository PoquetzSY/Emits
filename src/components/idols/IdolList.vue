<template>
    <div class="list">
        <IdolItem v-for="idol in Idols" :key="idol.id" v-bind="idol"></IdolItem>
    </div>
</template>

<script setup lang="ts">
import IdolItem from './IdolItem.vue';
import Idols from '@/data/IdolData';
</script>

<style scoped>
.list {
    display: flex;
    flex-direction: column;
}
</style>
