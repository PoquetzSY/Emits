
<template>
    <div>
        <form @submit.prevent="addIdol">
            <div class="form">
                <label for="name">Name:</label>
                <input type="text" id="name" v-model="newIdol.name" required>
            </div>
            <div class="form">
                <label for="age">Age:</label>
                <input type="number" id="age" v-model="newIdol.age" required>
            </div>
            <div class="form">
                <label for="group">Group:</label>
                <input type="text" id="group" v-model="newIdol.group" required>
            </div>
            <button type="submit">Add Idol</button>
        </form>

        <ul>
            <li v-for="idol in idols" :key="idol.id">
                {{ idol.name }} - {{ idol.age }} - {{ idol.group }}
            </li>
        </ul>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import type { IIDolInfo } from '@/interfaces/IIdolInfo';

const idols = ref<IIDolInfo[]>([
    { id: 1, name: 'Idol 1', age: 20, group: 'Group 1' },
    { id: 2, name: 'Idol 2', age: 22, group: 'Group 2' },
]);

const newIdol = ref<IIDolInfo>({
    id: 0,
    name: '',
    age: 0,
    group: '',
});

function addIdol() {
    newIdol.value.id = idols.value.length + 1;
    idols.value.push({ ...newIdol.value });
    newIdol.value.name = '';
    newIdol.value.age = 0;
    newIdol.value.group = '';
}
</script>

<style scoped>
.form {
    margin: 1rem 0;
}
</style>