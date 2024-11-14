<script setup>
import DropDown from './components/DropDown.vue';
import { ref } from 'vue';

const cityNames = ref([
  "連江縣","金門縣","宜蘭縣",
  "新竹縣","苗栗縣","彰化縣",
  "南投縣","雲林縣","嘉義縣",
  "屏東縣","臺東縣","花蓮縣",
  "澎湖縣","基隆市","新竹市",
  "嘉義市","臺北市","高雄市",
  "新北市","臺中市","台南市",
  "桃園市"
]);
</script>

<template>
  <DropDown :city-names="cityNames"/>
</template>

<style scoped>
@media (max-width: 600px) {}
@media (min-width: 601px) and (max-width: 768px) {}
@media (min-width: 769px) and (max-width: 900px) {}
@media (min-width: 901px) and (max-width: 1024px) {}
@media (min-width: 1025px) {}
</style>
