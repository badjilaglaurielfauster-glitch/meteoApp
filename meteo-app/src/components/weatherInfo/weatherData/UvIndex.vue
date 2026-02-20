<script setup>
import {computed} from 'vue'

const props = defineProps({
  uvIndex: Number
})

const uvLevel = computed(() =>{
  if (props.uvIndex <= 2) return 'Faible'
  if (props.uvIndex >= 3 && props.uvIndex <= 5) return 'Modéré (Mettez un chapeau et de la crème solaire)'
  if (props.uvIndex >= 6 && props.uvIndex <= 7) return 'Élevé (Attention danger)'
  if (props.uvIndex >= 8 && props.uvIndex <= 10) return 'Très élevé'
  return 'Extrême'
})



</script>

<template>
  <div class="uv-index">
    <h3>Indice UV: {{ uvIndex }}</h3>
    <p>Niveau: {{ uvLevel }}</p>
  </div>

</template>

<style scoped>
.uv-index {
  background-color: #f0f8ff;
  padding: 10px;
  border-radius: 5px;
  margin: 10px 0;
}
.uv-index h3 {
  margin: 0;
}
.uv-index p {
  margin: 5px 0;
}
</style>
