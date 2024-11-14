<script setup>
import ImageWeather from './ImageWeather.vue';
import { ref, watch } from 'vue';

const props = defineProps({
  cityName: String
});

let forecast;

const dataUrl = "/api/forecast.json";
$.ajax({
    url: dataUrl,
    method: 'GET',
    dataType: 'json',
    data: '',
    async: false,
    success: (res) => {
        forecast = res;
    },
    error: (err) => {
        console.log(err);
    },
});

const weatherStatus = ref(forecast["data"][11]["Wx"]["elementValue"][0]["value"]);
const averageTemperature = ref(forecast["data"][11]["T"]["elementValue"]["value"] + "°C");
const minMaxTemperature = ref("Min : " + forecast["data"][11]["MinT"]["elementValue"]["value"] + " °C"
                          + " / "
                          + "Max : " + forecast["data"][11]["MaxT"]["elementValue"]["value"] + " °C");
watch(
  () => props.cityName,
  (newVal, oldVal) => {
    forecast["data"].forEach(area => {
        if (area["location"] === newVal) {
            weatherStatus.value = area["Wx"]["elementValue"][0]["value"];
            averageTemperature.value = area["T"]["elementValue"]["value"] + "°C";
            minMaxTemperature.value = "Min : " + area["MinT"]["elementValue"]["value"] + " °C"
                                      + " / "
                                      + "Max : " + area["MaxT"]["elementValue"]["value"] + " °C";
        }
    });
  }
);
</script>

<template>
    <ImageWeather :weather-status="weatherStatus"/>
    <div id="temperature-box">
        <div id="text-average">{{ averageTemperature }}</div>
        <div id="text-min-max">{{ minMaxTemperature }}</div>
    </div>
</template>

<style scoped>
#temperature-box {
    margin-top: 75px;
    margin-left: 75px;
}

#text-average {
    display: flex;
    justify-content: center;
    font-size: 70px;
    font-weight: 500;
}

#text-min-max {
    display: flex;
    justify-content: center;
    font-weight: 400;
    font-size: 15px;
    margin-top: 20px;
}

@media (max-width: 600px) {
    #temperature-box {
        margin-top: 20px;
        margin-left: 0px;
    }
}
@media (min-width: 601px) and (max-width: 768px) {}
@media (min-width: 769px) and (max-width: 900px) {}
@media (min-width: 901px) and (max-width: 1024px) {}
@media (min-width: 1025px) {}
</style>