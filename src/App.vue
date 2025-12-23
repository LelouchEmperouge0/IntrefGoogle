<!-- src/App.vue -->
<template>
  <div class="min-h-screen bg-gradient-to-b from-gray-50 to-white flex flex-col items-center px-4 py-10 sm:py-16">
    <h1 class="text-4xl sm:text-5xl font-bold mb-8 tracking-tight">
      <span class="text-blue-500">G</span>
      <span class="text-red-500">o</span>
      <span class="text-yellow-500">o</span>
      <span class="text-blue-500">g</span>
      <span class="text-green-500">l</span>
      <span class="text-red-500">e</span>
    </h1>

    <SearchBar @search="handleSearch" class="w-full max-w-2xl" />

    <div v-if="results" class="mt-10 w-full max-w-3xl animate-fade-in">
      <SearchResult :result="results" @related-query-click="handleSearch" />
    </div>

    <div v-else-if="error" class="mt-10 text-gray-600 text-center max-w-lg px-4">
      Aucun résultat pour «&nbsp;{{ error }}&nbsp;». Essayez un autre mot.
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import SearchBar from './components/SearchBar.vue'
import SearchResult from './components/SearchResult.vue'
import data from './data/data.json'

const results = ref(null)
const error = ref(null)

const handleSearch = (query) => {
  const key = query.trim().toLowerCase()
  if (data[key]) {
    results.value = data[key]
    error.value = null
  } else {
    results.value = null
    error.value = query.trim()
  }
  window.scrollTo({ top: document.body.scrollHeight, behavior: 'smooth' })
}
</script>

<style>
.animate-fade-in {
  animation: fadeIn 0.35s ease-out;
}
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(8px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>