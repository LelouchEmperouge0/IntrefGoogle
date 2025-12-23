
<template>
  <div class="absolute z-20 w-full mt-2 bg-white rounded-xl shadow-lg border border-gray-200 overflow-hidden">
    <div
      v-for="suggestion in suggestions"
      :key="suggestion"
      @click="$emit('select', suggestion)"
      class="px-4 py-2.5 hover:bg-gray-50 cursor-pointer text-gray-800 transition-colors"
    >
      {{ suggestion }}
    </div>
  </div>
</template>

<script setup>
defineProps({
  suggestions: { type: Array, required: true }
})
defineEmits(['select'])
</script>