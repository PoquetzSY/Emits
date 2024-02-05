<template>
    <form @submit.prevent="addIdol">
        <div class="form">
            <label for="name">Name:</label>
            <input type="text" id="name" v-model="name" required>
        </div>
        <div class="form">
            <label for="lastName">Last Name:</label>
            <input type="text" id="lastName" v-model="lastName" required>
        </div>
        <div class="form">
            <label for="age">Age:</label>
            <input type="number" id="age" v-model="age" required>
        </div>
        <div class="form">
            <label for="nationality">nationality:</label>
            <input type="text" id="nationality" v-model="nationality" required>
        </div>
        <div class="form">
            <label for="birthdate">Birthdate:</label>
            <input type="date" id="birthdate" v-model="birthdate" required>
        </div>
        <div class="form">
            <label for="photo">Photo:</label>
            <input type="text" id="photo" v-model="photo" required>
        </div>
        <div class="form">
            <label for="color">Color:</label>
            <input type="text" id="color" v-model="color" required>
        </div>
        <div class="form">
            <label for="group">Group:</label>
            <input type="text" id="group" v-model="group" required>
        </div>
        <div class="form">
            <label for="colorGroup">Color Group:</label>
            <input type="text" id="colorGroup" v-model="colorGroup" required>
        </div>
        <div class="form">
            <label for="role">Role:</label>
            <input type="text" id="role" v-model="role" required>
        </div>
        <button type="submit">Add Idol</button>
    </form>
</template>

<script setup lang="ts">
import { defineEmits, ref } from "vue";
import type { IIDolInfo } from '@/interfaces/IIdolInfo';
import Idols from '@/data/IdolData';

const name = ref('');
const lastName = ref('');
const age = ref(0);
const nationality = ref('');
const birthdate = ref('');
const photo = ref('');
const color = ref('');
const group = ref('');
const colorGroup = ref('');
const role = ref('');


const newIdol = ref<IIDolInfo>({
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
const emit = defineEmits(['addIdol']);
function addIdol() {
    newIdol.value.id = Idols.length + 1;
    newIdol.value.name = name.value;
    newIdol.value.lastName = lastName.value;
    newIdol.value.age = age.value;
    newIdol.value.nationality = nationality.value;
    newIdol.value.birthdate = birthdate.value;
    newIdol.value.photo = photo.value;
    newIdol.value.color = color.value;
    newIdol.value.group = group.value;
    newIdol.value.colorGroup = colorGroup.value;
    newIdol.value.role = role.value;
    Idols.push({ ...newIdol.value });
    emit('addIdol', { ...newIdol.value });
    console.log(Idols);
}

</script>

<style scoped>
.modal-mask {
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
}

.modal-container {
    width: 300px;
    margin: 150px auto;
    padding: 20px 30px;
    background-color: #616161;
    border-radius: 2px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
}
</style>stylestyle