<script setup lang="ts">
import route from '@/router';
import NavItem from './NavItem.vue';
const routes = route.options.routes
</script>
<template>
    <nav>
        <NavItem v-for="route in routes" :key="route.name || ''" :path="route.path" :name="(route.name as string)" />
    </nav>
</template>

<style scoped>
nav {
    width: 100%;
    font-size: 12px;
    text-align: center;
    margin-top: 2rem;
}

@media (min-width: 1024px) {
    nav {
        text-align: left;
        margin-left: -1rem;
        font-size: 1rem;

        padding: 1rem 0;
        margin-top: 1rem;
    }
}
</style>