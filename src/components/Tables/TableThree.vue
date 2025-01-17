<script setup lang="ts">
import { ref, computed } from 'vue'

const packages = ref([
  {
    name: 'PDF 1',
    uploadDate: new Date('2025-01-13T10:00:00Z'),
    status: true,
    department: 'HR',
    deme: 'A',
    sop: 'SOP1'
  },
  {
    name: 'PDF 2',
    uploadDate: new Date('2025-01-13T12:00:00Z'),
    status: false,
    department: 'Finance',
    deme: 'B',
    sop: 'SOP2'
  },
  {
    name: 'PDF 3',
    uploadDate: new Date('2025-01-13T14:15:00Z'),
    status: false,
    department: 'IT',
    deme: 'A',
    sop: 'SOP3'
  },
  {
    name: 'PDF 4',
    uploadDate: new Date('2025-01-13T16:00:00Z'),
    status: true,
    department: 'HR',
    deme: 'B',
    sop: 'SOP1'
  }
])

const departments = ['HR', 'Finance', 'IT']
const demes = ['A', 'B']
const sops = ['SOP1', 'SOP2', 'SOP3']

const selectedDepartment = ref('')
const selectedDeme = ref('')
const selectedSop = ref('')

const filteredPackages = computed(() => {
  return packages.value.filter((pkg) => {
    return (
      (selectedDepartment.value === '' || pkg.department === selectedDepartment.value) &&
      (selectedDeme.value === '' || pkg.deme === selectedDeme.value) &&
      (selectedSop.value === '' || pkg.sop === selectedSop.value)
    )
  })
})

// Function to toggle the status of a file
const toggleStatus = (index) => {
  packages.value[index].status = !packages.value[index].status
}

// Format the date to include time
const formatDate = (date) => {
  return new Date(date).toLocaleString('en-US', {
    dateStyle: 'medium',
    timeStyle: 'short'
  })
}
</script>

<template>
  <div
    class="rounded-sm border border-stroke bg-white px-5 pt-6 pb-2.5 shadow-default dark:border-strokedark dark:bg-boxdark sm:px-7.5 xl:pb-1"
  >
    <!-- Filter Form -->
    <div class="mb-4 flex gap-4">
      <div>
        <label for="department" class="block text-sm font-medium text-gray-700 dark:text-white"
          >Department</label
        >
        <select
          id="department"
          v-model="selectedDepartment"
          class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm"
        >
          <option value="">All</option>
          <option v-for="department in departments" :key="department" :value="department">
            {{ department }}
          </option>
        </select>
      </div>
      <div>
        <label for="deme" class="block text-sm font-medium text-gray-700 dark:text-white"
          >Deme</label
        >
        <select
          id="deme"
          v-model="selectedDeme"
          class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm"
        >
          <option value="">All</option>
          <option v-for="deme in demes" :key="deme" :value="deme">{{ deme }}</option>
        </select>
      </div>
      <div>
        <label for="sop" class="block text-sm font-medium text-gray-700 dark:text-white">SOP</label>
        <select
          id="sop"
          v-model="selectedSop"
          class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm"
        >
          <option value="">All</option>
          <option v-for="sop in sops" :key="sop" :value="sop">{{ sop }}</option>
        </select>
      </div>
    </div>

    <div class="max-w-full overflow-x-auto">
      <table class="w-full table-auto">
        <thead>
          <tr class="bg-gray-100 text-left dark:bg-gray-800">
            <th class="min-w-[220px] py-4 px-4 font-medium text-black dark:text-white xl:pl-11">
              File Name
            </th>
            <th class="min-w-[200px] py-4 px-4 font-medium text-black dark:text-white">
              Upload Date & Time
            </th>
            <th class="min-w-[150px] py-4 px-4 font-medium text-black dark:text-white">Status</th>
            <th class="min-w-[150px] py-4 px-4 font-medium text-black dark:text-white">
              Department
            </th>
            <th class="min-w-[150px] py-4 px-4 font-medium text-black dark:text-white">Deme</th>
            <th class="min-w-[150px] py-4 px-4 font-medium text-black dark:text-white">SOP</th>
            <th class="min-w-[150px] py-4 px-4 font-medium text-black dark:text-white">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(pkg, index) in filteredPackages"
            :key="index"
            class="border-b border-stroke dark:border-strokedark"
          >
            <td class="py-4 px-4">{{ pkg.name }}</td>
            <td class="py-4 px-4">{{ formatDate(pkg.uploadDate) }}</td>
            <td class="py-4 px-4">
              <span :class="pkg.status ? 'text-green-500' : 'text-red-500'">
                {{ pkg.status ? 'Active' : 'Inactive' }}
              </span>
            </td>
            <td class="py-4 px-4">{{ pkg.department }}</td>
            <td class="py-4 px-4">{{ pkg.deme }}</td>
            <td class="py-4 px-4">{{ pkg.sop }}</td>
            <td class="py-4 px-4">
              <button
                @click="toggleStatus(index)"
                class="px-4 py-2 text-sm font-medium text-white bg-blue-500 rounded hover:bg-blue-600"
              >
                Toggle
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
/* Add any necessary styles here */
</style>
