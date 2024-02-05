<template>
    <div class="card" :style="{ background: 'linear-gradient(to right, ' + cardColor + ')', color: textColor }">
        <div>
            <p># {{ props.id }}</p>
            <h2>{{ props.lastName }} {{ props.name }}</h2>
            <p>{{ props.age }} Años</p>
            <p>{{ props.birthdate }}</p>
            <p>{{ props.group }}</p>
            <p>{{ props.role }}</p>
            <div class="colors">
                <div>
                    <p>Color Idol</p>
                    <button :style="{ background: 'linear-gradient(to right, ' + props.color +','+ props.color + ')' }" class="btn"
                        @click="changeCardColor(props.color)"></button>
                </div>
                <div>
                    <p>Color Grupo</p>
                    <button :style="{ background: 'linear-gradient(to right, ' + props.colorGroup + ')' }" class="btn"
                        @click="changeCardColor(props.colorGroup)"></button>
                </div>
            </div>
        </div>

        <div>
            <img :src="props.photo" :alt="props.name">
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import type { IIDolInfo } from '@/interfaces/IIdolInfo';

const props = defineProps<IIDolInfo>();
const cardColor = ref('');
const textColor = ref('');

function changeCardColor(color: string) {
    if (color.includes(',')) {
        cardColor.value = color;
        changeTextColor(color.split(',')[0]);
    } else {
        cardColor.value = color + ',' + color;
        changeTextColor(color);
    }
}
function changeTextColor(color: string) {
    if (color === 'black' || color === '#2253a3') {
        textColor.value = 'white';
    } else {
        textColor.value = 'black';
    }
}
</script>

<style scoped>
.card {
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    border-radius: 12px;
    margin: 1rem 0;
    padding: 1rem;
    display: flex;
    justify-content: space-between;
    background-color: #616161;
    color: black;
}

img {
    width: 150px;
    border-radius: 7.5px;
}

.btn {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    border: none;
    margin: 0;
    padding: 0;
    cursor: pointer;
    transition: all 0.3s;
}

.colors {
    display: flex;
}

.colors div {
    margin-top: 10px;
    margin-right: 2rem;
}
</style>
