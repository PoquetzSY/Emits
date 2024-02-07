<template>
    <form @submit.prevent="addIdol" class="form-container" autocomplete="off">
        <div class="form-group">
            <div>
                <label for="name">Nombre:</label>
                <input :class="{errorInput:ers.nameE || ers.nameC }" @input="nameValidation()" type="text" id="name" v-model.trim="newIdol.name" required >
                <p v-if="ers.nameE">Rellene este campo</p>
                <p v-if="ers.nameC">Caracteres invalidos</p>
            </div>
            <div>
                <label for="lastName">Apellido:</label>
                <input :class="{errorInput:ers.lNameE || ers.lNameC }" @input="lastNameValidation()" type="text" id="lastName" v-model.trim="newIdol.lastName" required >
                <p v-if="ers.lNameE">Rellene este campo</p>
                <p v-if="ers.lNameC">Caracteres invalidos</p>
            </div>
            <div>
                <label for="age">Edad:</label>
                <input type="number" id="age" v-model="newIdol.age" required >
                <p v-if="ers.ageE">Rellene este campo</p>
                <p v-if="ers.ageC">Edad invalida</p>
            </div>
        </div>
        <div class="form-group">
            <div>
                <label for="nationality">Nacionalidad:</label>
                <input :class="{errorInput:ers.nacionalityE || ers.nacionalityC }" @input="nacionalityValidation()" type="text" id="nationality" v-model.trim="newIdol.nationality" required >
                <p v-if="ers.nacionalityE">Rellene este campo</p>
                <p v-if="ers.nacionalityC">Caracteres invalidos</p>
            </div>
            <div>
                <label for="birthdate">Fecha de nacimiento:</label>
                <input type="date" id="birthdate" v-model="newIdol.birthdate" required >
            </div>
            <div>
                <label for="role">Rol en el Grupo:</label>
                <input :class="{errorInput:ers.roleE || ers.roleC }" @input="roleValidation()" type="text" id="role" v-model.trim="newIdol.role" required >
                <p v-if="ers.roleE">Rellene este campo</p>
                <p v-if="ers.roleC">Caracteres invalidos</p>
            </div>
        </div>
        <div class="form-group">
            <div>
                <label for="photo">Imagen:</label>
                <input type="text" id="photo" v-model="newIdol.photo" required >
            </div>
        </div>
        <div class="form-group">
            <div>
                <label for="color">Color del Idol:</label>
                <input type="text" id="color" v-model="newIdol.color" required >
            </div>
            <div>
                <label for="group">Grupo al que pertenece:</label>
                <input :class="{errorInput:ers.groupE || ers.groupC }" @input="groupValidation()" type="text" id="group" v-model.trim="newIdol.group" required >
                <p v-if="ers.groupE">Rellene este campo</p>
                <p v-if="ers.groupC">Caracteres invalidos</p>
            </div>
            <div>
                <label for="colorGroup">Color del Grupo:</label>
                <input type="text" id="colorGroup" v-model="newIdol.colorGroup" required >
            </div>
        </div>
        <div class="btn">
            <button type="submit">Añadir Idol</button>
        </div>
    </form>
</template>

<script setup lang="ts">
import { defineEmits, reactive,ref } from "vue";
import type { IIDolInfo } from '@/interfaces/IIdolInfo';
import Idols from '@/data/IdolData';

const ers = reactive({
    nameE: false,
    nameC: false,
    lNameE: false,
    lNameC: false,
    nacionalityE: false,
    nacionalityC: false,
    roleE: false,
    roleC: false,
    groupE: false,
    groupC: false,
    ageE: false,
    ageC: false
});

const newIdol = reactive<IIDolInfo>({
    id: 0,
    name: '',
    age: null,
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
    if (!validationForm()) {
        return;
    }else{
        newIdol.id = Idols.length + 1;
        newIdol.color = newIdol.color + ',#616161';
        emit('add-Idol', { ...newIdol });
        console.log(Idols);
    }
}

function validationForm() {
    if (ers.nameE === true || ers.nameC === true || ers.lNameE === true || ers.lNameC === true || ers.nacionalityE === true || ers.nacionalityC === true || ers.roleE === true || ers.roleC === true || ers.groupE === true || ers.groupC === true) {
        return false;
    } else {
        return true;
    }
}

const nameValidation = () => {
    if (newIdol.name === '' ) {
        ers.nameE = true;
    } else {
        ers.nameE = false;
    }
    if (!/^[a-zA-Z\s]+$/.test(newIdol.name)) {
        ers.nameC = true;
    } else {
        ers.nameC = false;
    }
}

const lastNameValidation = () => {
    if (newIdol.lastName === '' ) {
        ers.lNameE = true;
    } else {
        ers.lNameE = false;
    }
    if (!/^[a-zA-Z\s]+$/.test(newIdol.lastName)) {
        ers.lNameC = true;
    } else {
        ers.lNameC = false;
    }
}

const nacionalityValidation = () => {
    if (newIdol.nationality === '' ) {
        ers.nacionalityE = true;
    } else {
        ers.nacionalityE = false;
    }
    if (!/^[a-zA-Z\s]+$/.test(newIdol.nationality)) {
        ers.nacionalityC = true;
    } else {
        ers.nacionalityC = false;
    }
}
const roleValidation = () => {
    if (newIdol.role === '' ) {
        ers.roleE = true;
    } else {
        ers.roleE = false;
    }
    if (!/^[a-zA-Z\s]+$/.test(newIdol.role)) {
        ers.roleC = true;
    } else {
        ers.roleC = false;
    }
}
const groupValidation = () => {
    if (newIdol.group === '' ) {
        ers.groupE = true;
    } else {
        ers.groupE = false;
    }
    if (!/^[a-zA-Z\s]+$/.test(newIdol.group)) {
        ers.groupC = true;
    } else {
        ers.groupC = false;
    }
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
    display: flex;
}

.form-group div {
    flex: 1;
    margin-right: 10px;
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
    border: none;
    border-radius: 4px;
    box-sizing: border-box;
    background-color: rgb(221, 221, 221);
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

.btn {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.errorInput {
    border: 2px solid red;
}
p {
    color: red;
}
</style>