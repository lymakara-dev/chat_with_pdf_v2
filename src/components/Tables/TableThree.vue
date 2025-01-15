<script setup lang="ts">
import { ref } from 'vue';

// Sample data with a status field
const packages = ref([
  { name: 'PDF 1', uploadDate: new Date('2025-01-13T10:30:00Z'), status: true },
  { name: 'PDF 2', uploadDate: new Date('2025-01-13T12:45:00Z'), status: false },
  { name: 'PDF 3', uploadDate: new Date('2025-01-13T14:15:00Z'), status: false },
  { name: 'PDF 4', uploadDate: new Date('2025-01-13T16:00:00Z'), status: true },
]);

// Function to toggle the status of a file
const toggleStatus = (index) => {
  packages.value[index].status = !packages.value[index].status;
};

// Format the date to include time
const formatDate = (date) => {
  return new Date(date).toLocaleString('en-US', {
    dateStyle: 'medium',
    timeStyle: 'short',
  });
};
</script>

<template>
  <div
    class="rounded-sm border border-stroke bg-white px-5 pt-6 pb-2.5 shadow-default dark:border-strokedark dark:bg-boxdark sm:px-7.5 xl:pb-1"
  >
    <div class="max-w-full overflow-x-auto">
      <table class="w-full table-auto">
        <thead>
          <tr class="bg-gray-2 text-left dark:bg-meta-4">
            <th class="min-w-[220px] py-4 px-4 font-medium text-black dark:text-white xl:pl-11">
              File Name
            </th>
            <th class="min-w-[200px] py-4 px-4 font-medium text-black dark:text-white">
              Upload Date & Time
            </th>
            <th class="min-w-[120px] py-4 px-4 font-medium text-black dark:text-white">
              Status
            </th>
            <th class="py-4 px-4 font-medium text-black dark:text-white">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in packages" :key="index">
            <td class="py-5 px-4 pl-9 xl:pl-11">
              <h5 class="font-medium text-black dark:text-white">{{ item.name }}</h5>
            </td>
            <td class="py-5 px-4">
              <p class="text-black dark:text-white">{{ formatDate(item.uploadDate) }}</p>
            </td>
            <td class="py-5 px-4">
              <label class="inline-flex items-center cursor-pointer">
                <input
                  type="checkbox"
                  class="sr-only"
                  :checked="item.status"
                  @change="toggleStatus(index)"
                />
                <div
                  class="relative w-10 h-6 bg-gray-200 rounded-full shadow-inner"
                  :class="{ 'bg-green-500': item.status, 'bg-red-500': !item.status }"
                >
                  <span
                    class="absolute left-1 top-1 w-4 h-4 bg-white rounded-full shadow transform transition-transform"
                    :class="{ 'translate-x-full': item.status }"
                  ></span>
                </div>
              </label>
            </td>
            <td class="py-5 px-4">
              <div class="flex items-center space-x-3.5">
                <button class="hover:text-primary">
                  <svg
                    class="fill-current"
                    width="18"
                    height="18"
                    viewBox="0 0 18 18"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    
                  </svg>
                </button>

                <button class="hover:text-primary">
                  <svg
                    class="fill-current"
                    width="18"
                    height="18"
                    viewBox="0 0 18 18"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                  
                  </svg>
                </button>

                <button class="hover:text-primary">
                  <svg
                    class="fill-current"
                    width="18"
                    height="18"
                    viewBox="0 0 18 18"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                  
                  </svg>
                </button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
