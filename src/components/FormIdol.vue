<template>
    <form @submit.prevent="addIdol" class="form-container" autocomplete="off">
        <div class="form-group">
            <div>
                <label for="name">Nombre:</label>
                <input :class="{errorInput:nameE || nameC }" @input="nameValidation()" type="text" id="name" v-model.trim="newIdol.name" required >
                <p v-if="nameE">Rellene este campo</p>
                <p v-if="nameC">Caracteres invalidos</p>
            </div>
            <div>
                <label for="lastName">Apellido:</label>
                <input :class="{errorInput:lNameE || lNameC }" @input="lastNameValidation()" type="text" id="lastName" v-model.trim="newIdol.lastName" required >
                <p v-if="lNameE">Rellene este campo</p>
                <p v-if="lNameC">Caracteres invalidos</p>
            </div>
            <div>
                <label for="age">Edad:</label>
                <input type="number" id="age" v-model="newIdol.age" required >
            </div>
        </div>
        <div class="form-group">
            <div>
                <label for="nationality">Nacionalidad:</label>
                <input :class="{errorInput:nacionalityE || nacionalityC }" @input="nacionalityValidation()" type="text" id="nationality" v-model.trim="newIdol.nationality" required >
                <p v-if="nacionalityE">Rellene este campo</p>
                <p v-if="nacionalityC">Caracteres invalidos</p>
            </div>
            <div>
                <label for="birthdate">Fecha de nacimiento:</label>
                <input type="date" id="birthdate" v-model="newIdol.birthdate" required >
            </div>
            <div>
                <label for="role">Rol en el Grupo:</label>
                <input :class="{errorInput:roleE || roleC }" @input="roleValidation()" type="text" id="role" v-model.trim="newIdol.role" required >
                <p v-if="roleE">Rellene este campo</p>
                <p v-if="roleC">Caracteres invalidos</p>
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
                <input :class="{errorInput:groupE || groupC }" @input="groupValidation()" type="text" id="group" v-model.trim="newIdol.group" required >
                <p v-if="groupE">Rellene este campo</p>
                <p v-if="groupC">Caracteres invalidos</p>
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

const nameE = ref(false);
const nameC = ref(false);
const lNameE = ref(false);
const lNameC = ref(false);
const nacionalityE = ref(false);
const nacionalityC = ref(false);
const roleE = ref(false);
const roleC = ref(false);
const groupE = ref(false);
const groupC = ref(false);

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
    if (nameE.value === true || nameC.value === true || lNameE.value === true || lNameC.value === true || nacionalityE.value === true || nacionalityC.value === true || roleE.value === true || roleC.value === true || groupE.value === true || groupC.value === true) {
        return false;
    } else {
        return true;
    }
}

const nameValidation = () => {
    if (newIdol.name === '' ) {
        nameE.value = true;
    } else {
        nameE.value = false;
    }
    if (!/^[a-zA-Z\s]+$/.test(newIdol.name)) {
        nameC.value = true;
    } else {
        nameC.value = false;
    }
}

const lastNameValidation = () => {
    if (newIdol.lastName === '' ) {
        lNameE.value = true;
    } else {
        lNameE.value = false;
    }
    if (!/^[a-zA-Z\s]+$/.test(newIdol.lastName)) {
        lNameC.value = true;
    } else {
        lNameC.value = false;
    }
}

const nacionalityValidation = () => {
    if (newIdol.nationality === '' ) {
        nacionalityE.value = true;
    } else {
        nacionalityE.value = false;
    }
    if (!/^[a-zA-Z\s]+$/.test(newIdol.nationality)) {
        nacionalityC.value = true;
    } else {
        nacionalityC.value = false;
    }
}
const roleValidation = () => {
    if (newIdol.role === '' ) {
        roleE.value = true;
    } else {
        roleE.value = false;
    }
    if (!/^[a-zA-Z\s]+$/.test(newIdol.role)) {
        roleC.value = true;
    } else {
        roleC.value = false;
    }
}
const groupValidation = () => {
    if (newIdol.group === '' ) {
        groupE.value = true;
    } else {
        groupE.value = false;
    }
    if (!/^[a-zA-Z\s]+$/.test(newIdol.group)) {
        groupC.value = true;
    } else {
        groupC.value = false;
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