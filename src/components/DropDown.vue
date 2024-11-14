<script setup>
import WeatherArea from './WeatherArea.vue';
import { ref } from 'vue';

const props = defineProps({
  cityNames: Array
})

const selected = ref("花蓮縣");
</script>

<template>
    <div class="dropdown">
        <select class="select-style" v-model="selected">
            <option v-for="(city, index) in props.cityNames" :value="city">{{ city }}</option>
        </select>
    </div>

    <WeatherArea :city-name="selected"/>
</template>

<style scoped>
.dropdown {
    min-width: 250px;
    height: 50px;
    display: flex;
    justify-content: center;
    position: relative;
    margin-top: 110px;
}

.select-style {
    border: none;
    padding: 0 30px 0 15px;
    font-size: 30px;
    font-weight: bold;
}

@media (max-width: 600px) {}
@media (min-width: 601px) and (max-width: 768px) {}
@media (min-width: 769px) and (max-width: 900px) {}
@media (min-width: 901px) and (max-width: 1024px) {}
@media (min-width: 1025px) {}
</style>