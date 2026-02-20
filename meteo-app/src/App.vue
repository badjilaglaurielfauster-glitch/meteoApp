<script setup>

import { ref } from 'vue'
import axios from 'axios'
import SearchInput from './components/weatherInfo/SearchInput.vue'
import WeatherView from './components/weatherInfo/WeatherView.vue'

const weatherData = ref(null)
const error = ref(null)
const status = ref('')

const lookWeather = async ({city, apiKey}) => {
  try {
    status.value = 'Chargement...'
    error.value = null

    const response = await axios.get(
      'https://api.weatherapi.com/v1/forecast.json',
      {
        params: {
          key: apiKey, // 🔑 remplace par ta clé
          q: city,
          days: 4,
          lang: 'fr'
        }
      }
    )

    weatherData.value = response.data
    status.value = 'Importation réussie !'
  } catch (err) {
    error.value = 'Ville non trouvée ou erreur réseau.'
    status.value = ''
    weatherData.value = null
  }
}
</script>


<template>

   <div class="app-container">
    <h1>Weather App</h1>

    <SearchInput @search="lookWeather" />
    <WeatherView v-if="weatherData" :weatherData="weatherData" />


  </div>


</template>

<style scoped>

</style>
