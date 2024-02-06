<template>
    <h1>Lista de Idols registrados</h1>
    <div class="list">
        <IdolItem v-for="idol in idols" :key="idol.id" v-bind="idol"></IdolItem>
    </div>
</template>

<script setup lang="ts">

import IdolItem from './IdolItem.vue';
import { defineProps } from 'vue';
import type { IIDolInfo } from '@/interfaces/IIdolInfo';

defineProps<{
    idols: IIDolInfo[]
}>();

</script>

<style scoped>
.list {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    margin: 1rem 0;
}
</style>
