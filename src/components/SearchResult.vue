
<template>
  <div class="bg-white rounded-xl p-5 sm:p-6 shadow-sm border border-gray-200">
    <a :href="result.url" target="_blank" class="block no-underline">
      <h2 class="text-base sm:text-lg font-semibold text-blue-600 hover:underline">{{ result.title }}</h2>
      <p class="text-xs sm:text-sm text-green-700 mt-0.5 truncate">{{ result.url }}</p>
      <p class="text-gray-700 mt-2 text-sm sm:text-base leading-relaxed">{{ result.description }}</p>
    </a>

    
    <div v-if="result.relatedQueries?.length" class="mt-5">
      <p class="text-xs text-gray-500 mb-2">Requêtes associées :</p>
      <div class="flex flex-wrap gap-1.5">
        <button
          v-for="(query, i) in result.relatedQueries"
          :key="i"
          @click="$emit('related-query-click', query)"
          class="text-xs px-2.5 py-1 bg-gray-100 hover:bg-gray-200 rounded-full text-gray-700 transition-colors"
        >
          {{ query }}
        </button>
      </div>
    </div>

   
    <PeopleAlsoAsk v-if="result.peopleAlsoAsk" :questions="result.peopleAlsoAsk" class="mt-6" />
  </div>
</template>

<script setup>
import PeopleAlsoAsk from './PeopleAlsoAsk.vue'
defineProps({ result: Object })
defineEmits(['related-query-click'])
</script>