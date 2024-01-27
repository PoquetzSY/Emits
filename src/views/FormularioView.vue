<script setup lang="ts">

import { ref, computed } from 'vue';

const name = ref('');
const last_name = ref('');
const age = ref('');
const selectedGender = ref('');


const error_name = ref(false);
const error_lName = ref(false);
const error_same_name = ref(false);
const error_age = ref(false);

const Namevalidation = () => {
    if (name.value.length < 5) {
        error_name.value = true;

    } else {
        error_name.value = false;
    }
}
const LastNamevalidation = () => {
    if (last_name.value.length < 5) {
        error_lName.value = true;

    } else {
        error_lName.value = false;
    }
    if (last_name.value === name.value) {
        error_same_name.value = true;
    } else {
        error_same_name.value = false;
    }
}
const Agevalidation = () => {
    if (age.value > 60) {
        error_age.value = true;
    } else {
        error_age.value = false;
    }
}


const OtherSelected = computed(() => selectedGender.value === 'other');
</script>
<template>
    <div>
        <form class="form">

            <div>
                <label for="name">Nombre</label>
                <input @input="Namevalidation()" type="text" v-model="name" name="name" maxlength="18">
            </div>
            <p v-if="error_name" class="error">Minimo 5 caracteres</p>
            <div>
                <label for="last_name">Apellido</label>
                <input @input="LastNamevalidation()" type="text" v-model="last_name" name="last_name" maxlength="18">
            </div>
            <p v-if="error_lName" class="error">Minimo 5 caracteres</p>
            <p v-if="error_same_name" class="error">No puede ser igual al nombre</p>
            <div>
                <label for="age" class="age">Edad</label>
                <input @input="Agevalidation()" type="number" v-model="age" min="1" max="60" />
            </div>
            <p v-if="error_age" class="error">La edad maxima es 60 años</p>
            <div>
                <label for="gender">Genero</label>

                <div>
                    <input type="radio" id="man" value="man" v-model="selectedGender">
                    <label for="man">Hombre</label>

                    <input type="radio" id="woman" value="woman" v-model="selectedGender">
                    <label for="woman">Mujer</label>

                    <input type="radio" id="other" value="other" v-model="selectedGender">
                    <label for="other">Otro:</label>

                </div>
                <label v-if="OtherSelected" for="othergender">Especificar:</label>
                <input v-if="OtherSelected" type="text" name="othergender" maxlength="18">
            </div>

        </form>
    </div>
</template>


<style>
.form {
    width: 400px;
    font-size: 20px;
    display: flex;
    flex-direction: column;
}

.form input {
    background-color: var(--color-background);
    color: var(--color-text);
    border: none;
    border-bottom: 1px solid var(--color-text);
    ;
}

.form label {
    margin-right: 15px;
}

.error {
    color: red;
    font-size: 15px;

}

.age {
    padding-right: 29.31px;
}
</style>