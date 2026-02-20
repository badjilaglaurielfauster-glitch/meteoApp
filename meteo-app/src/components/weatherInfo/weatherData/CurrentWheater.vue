<script setup>
import { computed } from 'vue'

const props = defineProps({

  location: Object,
  current: Object
})


const iconUrl = computed(() => {
  return props.current.condition.icon.startsWith('http')
    ? props.current.condition.icon
    : `https:${props.current.condition.icon}`
})


const formattedTime = computed(() => {
  const date = new Date(props.location.localtime)
  return date.toLocaleTimeString('fr-FR', { hour: '2-digit', minute: '2-digit' })
})
</script>

<template>
  <div class="current-weather-card">
    <div class="header">
      <h2>{{ location.name }}</h2>
      <span class="time">Il est {{ formattedTime }}</span>
    </div>

    <div class="main-info">
      <img :src="iconUrl" :alt="current.condition.text" class="main-icon" />
      <div class="temp-container">
        <span class="temperature">{{ Math.round(current.temp_c) }}°</span>
        <span class="condition">{{ current.condition.text }}</span>
      </div>
    </div>

    <div class="feels-like">
      Ressenti : <strong>{{ Math.round(current.feelslike_c) }}°</strong>
    </div>
  </div>
</template>

<style scoped>
.current-weather-card {
  text-align: center;
  padding: 20px;
  background: linear-gradient(135deg, #6dd5ed, #2193b0); /* Un petit dégradé sympa */
  color: white;
  border-radius: 20px;
  margin-bottom: 20px;
  box-shadow: 0 10px 20px rgba(0,0,0,0.1);
}

.time {
  font-size: 0.9em;
  opacity: 0.8;
}

.main-info {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  margin: 20px 0;
}

.main-icon {
  width: 100px;
  height: 100px;
}

.temperature {
  font-size: 4em;
  font-weight: bold;
  display: block;
  line-height: 1;
}

.condition {
  font-size: 1.2em;
  text-transform: capitalize;
}

.feels-like {
  font-size: 1em;
  background: rgba(255, 255, 255, 0.2);
  display: inline-block;
  padding: 5px 15px;
  border-radius: 20px;
}
</style>
