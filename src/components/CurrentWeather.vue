
<script setup>
import { ref, computed, reactive } from "vue";

const apiKey = '621c72eb9edad6f8c9c010190a2403ea'
const host = 'api.openweathermap.org'
const resource = 'weather'
const lat = '52.4868'
const lon = '6.1228'
const units = 'metric'
const lang = 'nl'
const url = `https://${host}/data/2.5/${resource}?lat=${lat}&lon=${lon}&units=${units}c&lang=${lang}&appid=${apiKey}`

const weather = reactive(
    {
        data: null,
        isLoading: false,
        hasError: false
    }
)

const getWeather = () => {
    fetch(url)
        .then(response => response.json())
        .then(data => weather.data = data)
}


</script>

<template>
    <h2>Current weather</h2>

    <button @click="getWeather()">Get weather</button>
    <ul class="list">
        <li v-for="(key, index) in weather.data" :key="index">
            {{ index }} {{ key }}
        </li>
    </ul>
</template>

<style lang="scss" scoped>
main {
    display: flex;
    flex-direction: column;
    max-width: 500px;
    width: 100%;
    margin: 0 auto;
    padding: 40px 16px;

    h1 {
        margin-bottom: 16px;
        text-align: center;
    }

    .list {
        display: flex;
        flex-direction: column;
        list-style: none;
        margin-top: 24px;
        gap: 20px;
    }

    .todos-msg {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 8px;
        margin-top: 24px;
    }
}
</style>
