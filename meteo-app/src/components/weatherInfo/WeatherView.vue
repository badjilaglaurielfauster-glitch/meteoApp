<script setup>
import UvIndex from './weatherData/UvIndex.vue';
import WeatherDetails from './weatherData/WeatherDetails.vue';

defineProps({
  weatherData: Object
})

</script>

<template>
  <div class="weather-view">
    <WeatherDetails :label="weatherData."/>
    <UvIndex/>
  </div>

</template>

<style scoped>
</style>
