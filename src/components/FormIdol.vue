<template>
    <form @submit.prevent="addIdol" class="form-container">
        <div class="form-group">
            <label for="name">Nombre:</label>
            <input type="text" id="name" v-model="newIdol.name" required>
        </div>
        <div class="form-group">
            <label for="lastName">Apellido:</label>
            <input type="text" id="lastName" v-model="newIdol.lastName" required>
        </div>
        <div class="form-group">
            <label for="age">Edad:</label>
            <input type="number" id="age" v-model="newIdol.age" required>
        </div>
        <div class="form-group">
            <label for="nationality">Nacionalidad:</label>
            <input type="text" id="nationality" v-model="newIdol.nationality" required>
        </div>
        <div class="form-group">
            <label for="birthdate">Fecha de nacimiento:</label>
            <input type="date" id="birthdate" v-model="newIdol.birthdate" required>
        </div>
        <div class="form-group">
            <label for="photo">Imagen:</label>
            <input type="text" id="photo" v-model="newIdol.photo" required>
        </div>
        <div class="form-group">
            <label for="color">Color del Idol:</label>
            <input type="text" id="color" v-model="newIdol.color" required>
        </div>
        <div class="form-group">
            <label for="group">Grupo al que pertenece:</label>
            <input type="text" id="group" v-model="newIdol.group" required>
        </div>
        <div class="form-group">
            <label for="colorGroup">Color del Grupo:</label>
            <input type="text" id="colorGroup" v-model="newIdol.colorGroup" required>
        </div>
        <div class="form-group">
            <label for="role">Rol en el Grupo:</label>
            <input type="text" id="role" v-model="newIdol.role" required>
        </div>
        <button type="submit">Añadir Idol</button>
    </form>
</template>

<script setup lang="ts">
import { defineEmits, reactive } from "vue";
import type { IIDolInfo } from '@/interfaces/IIdolInfo';
import Idols from '@/data/IdolData';

const newIdol = reactive<IIDolInfo>({
    id: 0,
    name: '',
    age: 0,
    group: '',
    lastName: '',
    nationality: '',
    birthdate: '',
    photo: '',
    color: '',
    colorGroup: '',
    role: ''
});
const emit = defineEmits(['add-Idol']);

function addIdol() {
    newIdol.id = Idols.length + 1;
    newIdol.color = newIdol.color + ',#616161';
    emit('add-Idol', { ...newIdol });
    console.log(Idols);
}

</script>

<style scoped>
.form-container {
    width: 1000px;
    margin: auto;
    padding: 20px;
    background-color: #222;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    color: #fff;
}

.form-group {
    margin-bottom: 15px;
}

label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
}

input {
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
}

button {
    background-color: #3498db;
    color: #fff;
    padding: 10px 15px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

button:hover {
    background-color: #2980b9;
}
</style>