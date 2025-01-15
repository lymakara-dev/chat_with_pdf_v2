<template>
  <div class="flex flex-col items-center justify-center w-full min-h-screen bg-gray-100 text-gray-800 p-10">
    <!-- Component Start -->
    <div class="flex flex-col grow w-full max-w-4xl bg-white shadow-xl rounded-lg overflow-hidden">
      <div class="flex flex-col grow h-0 p-4 overflow-auto">
        <!-- Messages -->
        <div v-for="(message, index) in filteredMessages" :key="index" class="flex w-full mt-2 space-x-3" :class="{'justify-end': message.sender === 'user'}">
          <!-- Bot Message -->
          <div v-if="message.sender === 'bot'" class="flex-shrink-0 h-10 w-10 rounded-full bg-gray-300"></div>
          <div class="max-w-1/2">
            <div :class="{'bg-blue-600 text-white': message.sender === 'user', 'bg-gray-300': message.sender === 'bot'}" class="p-3 rounded">
              <p class="text-sm">{{ message.text }}</p>

              <div v-if="message.pdfs && message.pdfs.length > 0" class="mt-2">
                <div v-for="(pdf, pdfIndex) in message.pdfs" :key="pdfIndex" class="mt-2 border-t pt-2">
                  <p class="text-sm font-bold">{{ pdf.title }}</p>
                  <ul class="list-disc list-inside">
                    <li v-for="(page, pageIndex) in pdf.pages" :key="pageIndex">
                      Page {{ page.page }}: {{ page.keyword }}
                    </li>
                  </ul>
                  <div class="flex space-x-2 mt-2">
                    <a :href="'/path/to/' + pdf.title.replace(/ /g, '_') + '.pdf'" class="text-blue-500 underline" target="_blank">View PDF</a>
                    <a :href="'/path/to/' + pdf.title.replace(/ /g, '_') + '.pdf'" class="text-blue-500 underline" download>Download PDF</a>
                  </div>
                </div>
              </div>
            </div>
            <span class="text-xs text-gray-500 leading-none">{{ message.date }}</span>
          </div>
          <!-- User Message -->
          <div v-if="message.sender === 'user'" class="flex-shrink-0 h-10 w-10 rounded-full bg-blue-500"></div>
        </div>
      </div>

      <div class="bg-gray-200 p-2 flex items-center">
        <select v-model="selectedCategory" class="mr-2 p-2 rounded-lg">
          <option value="">Select Category</option>
          <option v-for="category in categories" :key="category" :value="category">{{ category }}</option>
        </select>
        <input type="date" v-model="selectedDate" class="mr-2 p-2 rounded-lg" />
        <input v-model="newMessage" class="flex items-center h-10 w-full rounded-xl px-3 text-sm" type="text" placeholder="Type your message…" />
        <button @click="sendMessage(newMessage)" class="ml-2 bg-blue-600 text-white px-4 py-2 rounded-lg">Send</button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';

const categories = ['General', 'Technical', 'Billing', 'Support'];
const selectedCategory = ref('');
const selectedDate = ref('');
const newMessage = ref('');

const messages = ref([
  { text: 'Hello', category: 'General', date: '2023-10-01', sender: 'user' },
  { text: 'Hello! How can I assist you today?', category: 'General', date: '2023-10-01', sender: 'bot' },
]);

const pdfs = ref([
  { title: 'Neural Networks Explained', category: 'Technical', date: '2023-10-01', pages: [{ page: 5, keyword: 'neural networks' }] },
  { title: 'Deep Learning Basics', category: 'Technical', date: '2023-10-01', pages: [{ page: 10, keyword: 'deep learning' }] },
]);

const filteredMessages = computed(() => {
  return messages.value.filter(message => {
    return (
      (selectedCategory.value === '' || message.category === selectedCategory.value) &&
      (selectedDate.value === '' || message.date === selectedDate.value)
    );
  });
});

const sendMessage = (text) => {
  if (text.trim() !== '') {
    const dateNow = new Date().toISOString().split('T')[0];
    messages.value.push({ text, category: selectedCategory.value, date: dateNow, sender: 'user' });
    generateResponse(text);
    newMessage.value = '';
  }
};

const generateResponse = (query) => {
  const responseText = `Here are some documents related to "${query}":`;
  const relevantPdfs = pdfs.value.filter(pdf => {
    return (
      (selectedCategory.value === '' || pdf.category === selectedCategory.value) &&
      (selectedDate.value === '' || pdf.date === selectedDate.value) &&
      pdf.pages.some(page => page.keyword.toLowerCase().includes(query.toLowerCase()))
    );
  });

  const response = {
    text: responseText,
    category: selectedCategory.value,
    date: new Date().toISOString().split('T')[0],
    sender: 'bot',
    pdfs: relevantPdfs,
  };

  messages.value.push(response);
};
</script>

<style scoped>
/* Custom styles */
</style>
