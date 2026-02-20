<script setup>
import { computed } from 'vue'

const props = defineProps({

  dayData: {
    type: Object,
    required: true
  }
})


const dayName = computed(() => {
  const date = new Date(props.dayData.date)
  return new Intl.DateTimeFormat('fr-FR', { weekday: 'long' }).format(date)
})


const iconUrl = computed(() => {
  const url = props.dayData.day.condition.icon
  return url.startsWith('http') ? url : `https:${url}`
})
</script>

<template>
  <div class="forecast-item">
    <span class="day-name">{{ dayName }}</span>

    <img :src="iconUrl" :alt="dayData.day.condition.text" class="weather-icon" />

    <div class="rain-chance">
      <span v-if="dayData.day.daily_chance_of_rain > 0">
        💧 {{ dayData.day.daily_chance_of_rain }}%
      </span>
    </div>

    <div class="temperatures">
      <span class="max">{{ Math.round(dayData.day.maxtemp_c) }}°</span>
      <span class="min">{{ Math.round(dayData.day.mintemp_c) }}°</span>
    </div>
  </div>
</template>

<style scoped>
.forecast-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #eee;
}

.day-name {
  width: 100px;
  text-transform: capitalize;
  font-weight: bold;
}

.weather-icon {
  width: 40px;
  height: 40px;
}

.rain-chance {
  width: 60px;
  font-size: 0.9em;
  color: #3498db;
}

.temperatures {
  width: 80px;
  text-align: right;
}

.max {
  font-weight: bold;
  margin-right: 8px;
}

.min {
  color: #7f8c8d;
}
</style>
