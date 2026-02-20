<script setup>

  import {ref} from 'vue'

  const city = ref('')
  const apiKey = ref('')
    const emit = defineEmits(['search'])

  const submitSearch = () =>{
    if(!city.value || !apiKey.value) return
    emit('search',{city: city.value, apiKey: apiKey.value})
    city.value = ''
    apiKey.value = ''
  }



</script>

<template>
  <div class="search-container">
    <input
      v-model="city"
      @keyup.enter="submitSearch"
      type="text"
      placeholder="Enter city name"
    />
    <input
      v-model="apiKey"
      @keyup.enter="submitSearch"
      type="text"
      placeholder="Enter API key"
    />
    <button @click="submitSearch">Search</button>
  </div>

</template>

<style scoped>
.search-container {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}
.search-container input {
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
}
.search-container button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #007BFF;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}


</style>
