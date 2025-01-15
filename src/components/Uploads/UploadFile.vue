<script setup lang="ts">
import { ref } from 'vue'
import DropdownSelect from '@/components/uploads/DropdownSelect.vue'

const departmentOptions = ['Sale', 'Loan', 'Credit', 'Finance', 'Marketing']
const documentTypeOptions = ['Memo', 'SOP', 'Policy', 'Procedure', 'Form']

const selectedDepartments = ref([])
const selectedDocumentTypes = ref([])

const handleDepartmentSelection = (selected) => {
  selectedDepartments.value = selected
}

const handleDocumentTypeSelection = (selected) => {
  selectedDocumentTypes.value = selected
}

const files = ref<File[]>([])
const previews = ref<string[]>([])

const handleFileChange = (event: Event) => {
  const input = event.target as HTMLInputElement
  if (input.files) {
    files.value = Array.from(input.files)
    previews.value = files.value.map(file => URL.createObjectURL(file))
  }
}

const deleteFile = (index: number) => {
  files.value.splice(index, 1)
  previews.value.splice(index, 1)
}

</script>

<template>
  <div class="flex flex-row gap-4">
    <div class="flex flex-col justify-center items-center gap-4 grow">
      <label for="file" class="font-bold text-2xl">Please upload your file</label>
      <div class="flex items-center justify-center w-full">
        <label
          for="dropzone-file"
          class="flex flex-col items-center justify-center w-full h-64 border-2 border-gray-300 border-dashed rounded-lg cursor-pointer bg-gray-50"
        >
          <div class="flex flex-col items-center justify-center pt-5 pb-6">
            <svg
              class="w-8 h-8 mb-4 text-gray-500 dark:text-gray-400"
              aria-hidden="true"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 20 16"
            >
              <path
                stroke="currentColor"
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M13 13h3a3 3 0 0 0 0-6h-.025A5.56 5.56 0 0 0 16 6.5 5.5 5.5 0 0 0 5.207 5.021C5.137 5.017 5.071 5 5 5a4 4 0 0 0 0 8h2.167M10 15V6m0 0L8 8m2-2 2 2"
              />
            </svg>
            <p class="mb-2 text-sm text-gray-500 dark:text-gray-400">
              <span class="font-semibold">Click to upload</span> or drag and drop
            </p>
            <p class="text-xs text-gray-500 dark:text-gray-400">
              SVG, PNG, JPG or GIF (MAX. 800x400px)
            </p>
          </div>
          <input id="dropzone-file" type="file" class="hidden" multiple @change="handleFileChange" />
        </label>
      </div>
      <div class="flex flex-wrap gap-4 mt-4">
        <div v-for="(preview, index) in previews" :key="index" class="relative w-32 h-32 border border-gray-300 rounded-lg overflow-hidden">
          <img :src="preview" alt="Preview" class="w-full h-full object-cover" />
          <button @click="deleteFile(index)" class="absolute top-1 right-1 bg-red-500 text-white rounded-full p-1">
            &times;
          </button>
        </div>
      </div>
    </div>

    <!-- Information Upload -->
    <div class="flex flex-col gap-4 items-center border-gray-300 border-2 rounded-lg p-4">
      <div class="grow flex flex-col gap-4">
        <h1 class="text-2xl font-bold">Input File Info</h1>
        <p class="text-base font-normal">Select Department</p>
        <DropdownSelect
          :options="departmentOptions"
          v-model:selected="selectedDepartments"
          @update:selected="handleDepartmentSelection"
        />
        
        <p class="text-base font-normal">Select Document Type</p>
        <DropdownSelect
          :options="documentTypeOptions"
          v-model:selected="selectedDocumentTypes"
          @update:selected="handleDocumentTypeSelection"
        />
      </div>
      <button
        type="button"
        class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
      >
        Upload
      </button>
    </div>
  </div>
</template>