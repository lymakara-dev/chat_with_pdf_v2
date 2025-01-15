<script setup lang="ts" name="ChatComponent"></script>

<template>
  <div
    class="flex flex-col items-center justify-center w-full min-h-screen bg-gray-100 text-gray-800 p-10"
  >
    <!-- Component Start -->
    <div class="flex flex-col grow w-full max-w-4xl bg-white shadow-xl rounded-lg overflow-hidden">
      <div class="flex flex-col grow h-0 p-4 overflow-auto">
        <div class="flex w-full mt-2 space-x-3 justify-end">
          <div class="">
            <div class="bg-blue-600 text-white p-3 rounded-l-lg rounded-br-lg">
              <p class="text-sm">Hello</p>
            </div>
            <span class="text-xs text-gray-500 leading-none">1 min ago</span>
          </div>
          <div class="flex-shrink-0 h-10 w-10 rounded-full bg-gray-300"></div>
        </div>
        <div class="flex w-full mt-2 space-x-3">
          <div class="flex-shrink-0 h-10 w-10 rounded-full bg-gray-300"></div>
          <div class="">
            <div class="bg-gray-300 p-3 rounded-r-lg rounded-bl-lg">
              <p class="text-sm">Hello! How can I assist you today?</p>
            </div>
            <span class="text-xs text-gray-500 leading-none">2 min ago</span>
          </div>
        </div>
        <!-- User Message -->
        <div class="flex w-full mt-2 space-x-3 justify-end">
          <div class="">
            <div class="bg-blue-600 text-white p-3 rounded-l-lg rounded-br-lg">
              <p class="text-sm">Can you explain the concept of neural networks from the PDF?</p>
            </div>
            <span class="text-xs text-gray-500 leading-none">1 min ago</span>
          </div>
          <div class="flex-shrink-0 h-10 w-10 rounded-full bg-gray-300"></div>
        </div>

        <!-- Bot Response -->
        <div class="flex w-full mt-2 space-x-3">
          <div class="flex-shrink-0 h-10 w-10 rounded-full bg-gray-300"></div>
          <div class="max-w-1/2">
            <div class="bg-gray-300 p-3 rounded-r-lg rounded-bl-lg">
              <p class="text-sm">
                Neural networks are a series of algorithms that attempt to recognize underlying
                relationships in a set of data through a process that mimics the way the human brain
                operates. They are used in a variety of applications, including image and speech
                recognition, and are a key component of deep learning algorithms.
              </p>
              <p class="text-sm mt-2">
                For a detailed explanation, please refer to the PDF document attached below.
              </p>
              <a href="/path/to/neural_networks.pdf" class="text-blue-500 underline mt-2"
                >View PDF</a
              >|
              <a href="/path/to/neural_networks.pdf" class="text-blue-500 underline mt-2"
                >Download PDF</a
              >
            </div>
            <span class="text-xs text-gray-500 leading-none">Just now</span>
          </div>
        </div>
      </div>
      <!-- Input Area -->
      <div class="bg-gray-200 p-2 flex items-center">
        <input
          class="flex items-center h-10 w-full rounded-xl px-3 text-sm"
          type="text"
          placeholder="Type your message…"
        />
        <button class="ml-2 bg-blue-600 text-white px-4 py-2 rounded-lg">Send</button>
      </div>
    </div>
  </div>
</template>
