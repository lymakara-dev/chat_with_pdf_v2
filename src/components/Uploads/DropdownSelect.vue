<template>
  <div class="relative inline-block text-left">
    <div>
      <button
        type="button"
        class="inline-flex w-50 justify-center gap-x-1.5 rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
        @click="toggleMenu"
      >
        {{ selectedDisplay }}
        <svg class="-mr-1 size-5 text-gray-400" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
          <path fill-rule="evenodd" d="M5.22 8.22a.75.75 0 0 1 1.06 0L10 11.94l3.72-3.72a.75.75 0 1 1 1.06 1.06l-4.25 4.25a.75.75 0 0 1-1.06 0L5.22 9.28a.75.75 0 0 1 0-1.06Z" />
        </svg>
      </button>
    </div>

    <div v-show="isMenuOpen" class="absolute right-0 z-10 mt-2 w-56 origin-top-right rounded-md bg-white shadow-lg ring-1 ring-black/5">
      <div class="py-1">
        <label v-for="(option, index) in options" :key="index" class="flex items-center px-4 py-2 hover:bg-gray-100">
          <input
            type="checkbox"
            :checked="selected.includes(option)"
            @change="toggleOption(option)"
            class="mr-2"
          />
          <span class="text-sm text-gray-700">{{ option }}</span>
        </label>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  options: {
    type: Array,
    default: () => []
  }
})

const emit = defineEmits(['update:selected'])

const isMenuOpen = ref(false)
const selected = ref([])

const selectedDisplay = computed(() => {
  return selected.value.length ? selected.value.join(', ') : 'Select options'
})

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const toggleOption = (option) => {
  const index = selected.value.indexOf(option)
  if (index === -1) {
    selected.value.push(option)
  } else {
    selected.value.splice(index, 1)
  }
  emit('update:selected', selected.value)
}
</script>