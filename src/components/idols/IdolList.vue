<template>
    <h1>Lista de Idols registrados</h1>
    <div class="list">
        <IdolItem v-for="idol in idols" :key="idol.id" v-bind="idol" @addIdol="addIdolE"></IdolItem>
    </div>
</template>

<script setup lang="ts">
import IdolItem from './IdolItem.vue';
import Idols from '@/data/IdolData';
import type { IIDolInfo } from '@/interfaces/IIdolInfo';
import { ref } from 'vue';

const idols = ref(Idols);

function addIdolE(idol: IIDolInfo) {
    idols.value.push(idol);
}

</script>

<style scoped>
.list {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    margin: 1rem 0;
}
</style>
