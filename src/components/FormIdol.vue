<template>
    <form @submit.prevent="addIdol" class="form-container" autocomplete="off">
        <div class="form-group">
            <div>
                <label for="name">Nombre:</label>
                <input :class="{ errorInput: ers.nameE || ers.nameC }" @input="nameValidation()" type="text" id="name"
                    v-model.trim="newIdol.name" required>
                <p v-show="ers.nameE">Rellene este campo</p>
                <p v-show="ers.nameC">Caracteres invalidos</p>
            </div>
            <div>
                <label for="lastName">Apellido:</label>
                <input :class="{ errorInput: ers.lNameE || ers.lNameC }" @input="lastNameValidation()" type="text"
                    id="lastName" v-model.trim="newIdol.lastName" required>
                <p v-show="ers.lNameE">Rellene este campo</p>
                <p v-show="ers.lNameC">Caracteres invalidos</p>
            </div>
            <div>
                <label for="age">Edad:</label>
                <input @input="ageValidation()" :class="{ errorInput: ers.ageE || ers.ageC }" type="number" id="age"
                    v-model.number="newIdol.age" required>
                <p v-show="ers.ageE">Rellene este campo</p>
                <p v-show="ers.ageC">Edad maxima es 60 años</p>
                <p v-show="ers.birthdateC">La edad no coincide con la fecha de nacimiento</p>

            </div>
        </div>
        <div class="form-group">
            <div>
                <label for="nationality">Nacionalidad:</label>
                <input :class="{ errorInput: ers.nacionalityE || ers.nacionalityC }" @input="nacionalityValidation()"
                    type="text" id="nationality" v-model.trim="newIdol.nationality" required>
                <p v-show="ers.nacionalityE">Rellene este campo</p>
                <p v-show="ers.nacionalityC">Caracteres invalidos</p>
            </div>
            <div>
                <label for="birthdate">Fecha de nacimiento:</label>
                <input @input="birthdateValidation()" :class="{ errorInput: ers.birthdateE || ers.birthdateC }" type="date"
                    id="birthdate" v-model="newIdol.birthdate" required>
                <p v-show="ers.birthdateE">Rellene este campo</p>
                <p v-show="ers.birthdateC">Fecha invalida, no coincide con la edad</p>
            </div>
            <div>
                <label for="role">Rol en el Grupo:</label>
                <input :class="{ errorInput: ers.roleE || ers.roleC }" @input="roleValidation()" type="text" id="role"
                    v-model.trim="newIdol.role" required>
                <p v-show="ers.roleE">Rellene este campo</p>
                <p v-show="ers.roleC">Caracteres invalidos</p>
            </div>
        </div>
        <div class="form-group">
            <div>
                <label for="photo">Imagen:</label>
                <input type="text" id="photo" v-model="newIdol.photo" required>
            </div>
        </div>
        <div class="form-group">
            <div>
                <label for="color">Color del Idol:</label>
                <input type="text" id="color" v-model="newIdol.color" required>
            </div>
            <div>
                <label for="group">Grupo al que pertenece:</label>
                <input :class="{ errorInput: ers.groupE || ers.groupC }" @input="groupValidation()" type="text" id="group"
                    v-model.trim="newIdol.group" required>
                <p v-show="ers.groupE">Rellene este campo</p>
                <p v-show="ers.groupC">Caracteres invalidos</p>
            </div>
            <div>
                <label for="colorGroup">Color del Grupo:</label>
                <input type="text" id="colorGroup" v-model="newIdol.colorGroup" required>
            </div>
        </div>
        <div class="btn">
            <button type="submit">Añadir Idol</button>
        </div>
    </form>
</template>

<script setup lang="ts">
import { defineEmits, reactive } from "vue";
import type { IIDolInfo } from '@/interfaces/IIdolInfo';
import Idols from '@/data/IdolData';


const idolEmpty = {
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
}
const newIdol = reactive<IIDolInfo>({ ...idolEmpty });
const emit = defineEmits(['add-Idol']);

function addIdol() {
    if (!validationForm()) {
        return;
    } else {
        newIdol.id = Idols.length + 1;
        newIdol.color = newIdol.color + ',#616161';
        emit('add-Idol', { ...newIdol });
        console.log(Idols);
    }
}

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
    ageC: false,
    birthdateE: false,
    birthdateC: false
});

function validationForm() {
    if (ers.nameE ||
        ers.nameC ||
        ers.lNameE ||
        ers.lNameC ||
        ers.nacionalityE ||
        ers.nacionalityC ||
        ers.roleE ||
        ers.roleC ||
        ers.groupE ||
        ers.groupC ||
        ers.ageE ||
        ers.ageC ||
        ers.birthdateE ||
        ers.birthdateC) {
        return false;
    } else {
        return true;
    }
}

const nameValidation = () => {
    if (newIdol.name === '') {
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
    if (newIdol.lastName === '') {
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
    if (newIdol.nationality === '') {
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
    if (newIdol.role === '') {
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
    if (newIdol.group === '') {
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
const ageValidation = () => {
    if (newIdol.age === null || newIdol.age <= 0) {
        ers.ageE = true;
    } else {
        ers.ageE = false;
        if (newIdol.age > 60) {
            ers.ageC = true;
        } else {
            ers.ageC = false;
        }
    }
}
const birthdateValidation = () => {
    const birthdate = Number(newIdol.birthdate.split('-')[0]) + (newIdol.age || 0);
    const nowYear = new Date().getFullYear();
    console.log(birthdate);

    if (newIdol.birthdate === '') {
        ers.birthdateE = true;
    } else {
        ers.birthdateE = false;
    }
    if (nowYear > birthdate || nowYear < birthdate) {
        ers.birthdateC = true;
    } else {
        ers.birthdateC = false;
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