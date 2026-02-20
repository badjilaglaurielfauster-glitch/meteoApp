<script setup>

  defineProps({
    label: String,
    value: Number,
    unit : String

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
