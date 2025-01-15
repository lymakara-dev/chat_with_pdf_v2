<script setup lang="ts">
import DropdownSelect from './DropdownSelect.vue'
</script>
<template>
  <div class="flex flex-row gap-4">
    <div class="flex flex-col justify-center items-center gap-4 grow">
      <label for="file" class="font-bold text-2xl">Please upload you file</label>
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
          <input id="dropzone-file" type="file" class="hidden" />
        </label>
      </div>
    </div>

    <!-- Information Upload -->
    <div class="flex flex-col gap-4 items-center border-gray-300 border-2 rounded-lg p-4">
      <div class="grow flex flex-col gap-4">
        <h1 class="text-2xl font-bold">Input File Info</h1>
        <DropdownSelect
          -options="Departement Option"
          -option1="Sale"
          -option2="Loan"
          -option3="Credit"
        />
        <DropdownSelect -options="Document Type" -option1="Memo" -option2="SOP" />
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
border-2 rounded-lg p-4
