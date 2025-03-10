<template>
    <div class="min-h-screen flex relative bg-surface-50 dark:bg-surface-950">
      <!-- Main Content -->
      <div class="min-h-screen flex flex-col relative flex-auto">
        <div class="h-[60px] flex justify-between lg:justify-start items-center px-8 bg-surface-0 dark:bg-surface-950 border-b border-surface relative lg:static">
          <div class="flex">
            <button @click="openModal" class="cursor-pointer block text-surface-700 dark:text-surface-100 mr-4 mt-1">
              <i class="pi pi-bars text-2xl" />
            </button>
          </div>
        </div>
  
        <div class="p-8 flex flex-col flex-auto">
          <div class="border-2 border-dashed rounded-border border-surface bg-surface-0 dark:bg-surface-950 flex-auto" />
        </div>
      </div>
  
      <!-- Modal -->
      <div v-if="isModalOpen" class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center" @click="closeModal">
        <!-- Prevent click from closing the modal when clicked inside -->
        <div class="bg-white dark:bg-surface-950 p-8 rounded-lg w-1/3" @click.stop>
          <div class="mb-4">
            <button @click="handleAction('Action 1')" class="w-full py-2 px-4 mb-2 bg-blue-500 text-white rounded">
              Action 1
            </button>
            <button @click="handleAction('Action 2')" class="w-full py-2 px-4 mb-2 bg-green-500 text-white rounded">
              Action 2
            </button>
            <button @click="handleAction('Action 3')" class="w-full py-2 px-4 mb-2 bg-yellow-500 text-white rounded">
              Action 3
            </button>
            <button @click="handleAction('Action 4')" class="w-full py-2 px-4 mb-2 bg-red-500 text-white rounded">
              Action 4
            </button>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  // Modal state
  const isModalOpen = ref(false);
  
  // Open modal
  const openModal = () => {
    isModalOpen.value = true;
  };
  
  // Close modal
  const closeModal = () => {
    isModalOpen.value = false;
  };
  
  // Handle button actions
  const handleAction = (action) => {
    console.log(`${action} clicked`);
    // Perform any action here based on the button clicked
  };
  </script>
  
  <style scoped>
  /* Add any additional styles here */
  </style>
  