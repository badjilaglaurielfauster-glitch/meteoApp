<script setup>
import CurrentWeather from './weatherData/CurrentWheater.vue'
import WeatherDetails from './weatherData/WeatherDetails.vue'
import UvIndex from './weatherData/UvIndex.vue'
import WheaterDay from './weatherData/WheaterDay.vue';

const props = defineProps({
  weatherData: {
    type: Object,
    required: true
  }
})
</script>

<template>
  <div class="weather-view" v-if="weatherData">

    <section class="hero-section">
      <CurrentWeather
        :location="weatherData.location"
        :current="weatherData.current"
      />
    </section>

    <section class="details-section">
      <div class="details-grid">
        <WeatherDetails
          label="Humidité"
          :value="weatherData.current.humidity"
          unit="%"
        />
        <UvIndex :uvIndex="weatherData.current.uv" />
        <WeatherDetails
          label="Vent"
          :value="weatherData.current.wind_kph"
          unit="km/h"
        />
        <WeatherDetails
          label="Précipitations"
          :value="weatherData.current.precip_mm"
          unit="mm"
        />
      </div>
    </section>

    <section class="forecast-section">
      <h3>Prévisions sur 3 jours</h3>
      <div class="forecast-container">
        <WheaterDay
          v-for="day in weatherData.forecast.forecastday"
          :key="day.date"
          :dayData="day"
        />
      </div>
    </section>
  </div>
</template>

<style scoped>
.weather-view {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}


.details-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 15px;
  margin-bottom: 30px;
}


.forecast-section {
  background: white;
  border-radius: 15px;
  padding: 20px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
}

.forecast-section h3 {
  margin-top: 0;
  margin-bottom: 15px;
  color: #2c3e50;
  font-size: 1.1rem;
  border-bottom: 2px solid #f0f2f5;
  padding-bottom: 10px;
}

.forecast-container {
  display: flex;
  flex-direction: column;
}


@media (max-width: 480px) {
  .details-grid {
    grid-template-columns: 1fr;
  }
}
</style>
