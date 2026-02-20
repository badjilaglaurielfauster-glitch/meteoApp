<script setup>

  defineProps({
    label: {
    type: String,
    required: true
  },
  value: {
    type: [Number, String],
    default: 0
  },
  unit: String
  })

</script>

<template>
  <div class="weather-detail">
    <span class="label">{{ label }}:</span>
    <span class="value">{{ value }} {{ unit }}</span>
  </div>
</template>

<style scoped>

</style>
