
<template>
  <div class="relative w-full">
    <div class="flex items-center bg-white rounded-full shadow ring-1 ring-gray-200 focus-within:ring-2 focus-within:ring-blue-300 transition-all duration-200 px-5 py-2.5">
      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-500 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
      </svg>
      <input
        v-model="input"
        @input="showSuggestions = true"
        @keyup.enter="submitSearch"
        @blur="hideSuggestions"
        type="text"
        class="w-full outline-none text-base placeholder-gray-500 bg-transparent"
        placeholder="Rechercher…"
        autocomplete="off"
      />
      <button @click="submitSearch" class="ml-1 text-gray-500 hover:text-gray-700">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 15l-6-6m6 6V9m0 0H9m6 6h6" />
        </svg>
      </button>
    </div>

    <AutoComplete
      v-if="showSuggestions"
      :suggestions="suggestions"
      @select="selectSuggestion"
    />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import AutoComplete from './AutoComplete.vue'
import data from '../data/data.json'

const emit = defineEmits(['search'])
const input = ref('')
const showSuggestions = ref(false)

const allKeys = Object.keys(data)

const suggestions = computed(() => {
  const q = input.value.trim().toLowerCase()
  return q ? allKeys.filter(k => k.includes(q)).slice(0, 5) : []
})

const hideSuggestions = () => {
  setTimeout(() => showSuggestions.value = false, 150)
}

const submitSearch = () => {
  if (input.value.trim()) {
    emit('search', input.value)
    showSuggestions.value = false
  }
}

const selectSuggestion = (suggestion) => {
  input.value = suggestion
  showSuggestions.value = false
  emit('search', suggestion)
}
</script>