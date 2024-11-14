<script setup>
import { ref, watch } from 'vue';

const props = defineProps({
  weatherStatus: String
});

const svgSrc = ref("/icon/weather-07.svg");

const objectMap = {
    "晴時多雲": '/icon/weather-02.svg',
    "陰天": '/icon/weather-07.svg'
};

watch(
  () => props.weatherStatus,
  (newVal, oldVal) => {
    svgSrc.value = objectMap[newVal];
  }
);
</script>

<template>
    <div id="status-box">
        <div id="img-container">
            <img :src="svgSrc" width="135" height="135" />
        </div>
        <div id="text-container">{{ weatherStatus }}</div>
    </div>
</template>

<style scoped>
#status-box {
    margin-top: 50px;
}

#img-container {
    display: flex;
    justify-content: center;
}

#text-container {
    display: flex;
    justify-content: center;
    font-weight: bold;
    font-size: 20px;
    margin-top: 20px;
}
</style>