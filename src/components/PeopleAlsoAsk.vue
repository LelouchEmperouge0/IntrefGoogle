<template>
  <div class="border-t border-gray-200 pt-4">
    <p class="text-sm font-medium text-gray-700 mb-3">Les gens demandent aussi</p>
    <div v-for="(item, index) in questions" :key="index" class="mb-3">
      <div
        @click="toggle(index)"
        class="flex items-center justify-between p-3 bg-gray-50 rounded-lg cursor-pointer hover:bg-gray-100 transition-colors duration-150"
      >
        <span class="text-gray-800">{{ item.question }}</span>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5 text-gray-500 transition-transform duration-200"
          :class="{ 'rotate-180': openIndex === index }"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
        </svg>
      </div>
      <div
        v-show="openIndex === index"
        class="mt-2 p-3 bg-gray-50 rounded-b-lg text-gray-700 text-sm leading-relaxed border-t border-gray-200"
      >
        {{ item.answer }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  questions: { type: Array, required: true }
})

const openIndex = ref(null)

const toggle = (index) => {
  openIndex.value = openIndex.value === index ? null : index
}
</script>