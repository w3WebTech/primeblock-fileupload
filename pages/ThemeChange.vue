<template>
  <div
    :class="isSidebarOpen || isFixedSidebar ? 'min-h-screen flex relative lg:static bg-[#f8fafc]' : 'min-h-screen flex relative lg:static bg-[#f8fafc]'">
    <div id="app-sidebar-10"
      class="h-full lg:h-auto flex-shrink-0 left-0 top-0 z-20 border-r border-surface transition-all duration-300"
      :class="isFixedSidebar ? 'w-[300px]' : 'w-0'" @mouseenter="openSidebar" @mouseleave="handleMouseLeave">
      <div class="flex h-full">
        <div class="flex flex-col h-full bg-[#2F449D] flex-shrink-0 select-none">
          <div class="flex items-center justify-between flex-shrink-0 h-[60px] mx-5">
            <div class="flex items-center justify-center">
              <svg height="36" viewBox="0 0 48 50" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" clip-rule="evenodd"
                  d="M33.1548 9.65956L23.9913 4.86169L5.54723 14.5106L0.924465 12.0851L23.9913 0L37.801 7.23403L33.1548 9.65956ZM23.9931 19.3085L42.4255 9.65955L47.0717 12.0851L23.9931 24.1595L10.1952 16.9361L14.8297 14.5106L23.9931 19.3085ZM4.6345 25.8937L0 23.4681V37.9149L23.0669 50V45.1489L4.6345 35.4894V25.8937ZM18.4324 28.2658L0 18.6169V13.7658L23.0669 25.8403V40.2977L18.4324 37.8615V28.2658ZM38.7301 23.468V18.6169L24.9205 25.8403V49.9999L29.555 47.5743V28.2659L38.7301 23.468ZM43.3546 35.4892V16.1914L48.0008 13.7659V37.9148L34.1912 45.1488V40.2977L43.3546 35.4892Z"
                  class="fill-[#FFFFFF]" />
              </svg>
            </div>
          </div>
          <div class="overflow-y-auto mt-4">
            <ul class="list-none py-4 pl-2 pr-0 m-0">
              <li class="mb-2" v-for="(item, index) in menuItems" :key="index">
                <a class="rounded-l-full flex items-center cursor-pointer py-4 pl-0 pr-2 justify-center hover:bg-[#3B55C4] text-[#FFFFFF] duration-150 transition-colors"
                  :class="{ 'bg-[#3B55C4]': activeTab2 === index }" @click="activeTab2 = index"
                  @mouseenter="changeActiveTab(index)">
                  <!-- Keep icon color consistent with text-[#FFFFFF] -->

                  <i :class="['text-xl', item.icon, 'text-[#FFFFFF]'

                    , { 'hover:text-gray-400': isSidebarOpen || isFixedSidebar }]" style="font-size: 1.5rem"></i>

                </a>
              </li>
            </ul>
          </div>
          <div class="mt-auto">
            <hr class="mb-4 mx-2 border-t border-0 border-[#FFFFFF]/20" />
            <a
              class="m-4 flex items-center cursor-pointer p-2 justify-center hover:bg-[#3B55C4] rounded-border text-[#cbd5e1] hover:text-[#ffffff] duration-150 transition-colors">
              <img
                src="https://fqjltiegiezfetthbags.supabase.co/storage/v1/render/image/public/block.images/blocks/avatars /circle/avatar-f-1.png"
                class="w-6 h-6" />
            </a>
          </div>
        </div>
        <div id="app-sidebar-10"
          class="h-full lg:h-auto flex-shrink-0 left-0 top-0 z-20 border-r border-surface bg-[#3B55C4] px-1 py-6"
          :class="{
            'w-[230px] opacity-100 fade-in': isSidebarOpen || isFixedSidebar, // When open, full width and fully visible
            'w-0 opacity-0 fade-out delay-150': !isSidebarOpen && !isFixedSidebar, // When closed, zero width and fully transparent
            'transition-all duration-3000 delay-150 ease-in-out': isSidebarOpen || isFixedSidebar, // 1-second smooth transition for all properties
            'lg:block': isFixedSidebar || isSidebarOpen, // Show for large screens when sidebar is open
            'lg:hidden': !isFixedSidebar && !isSidebarOpen // Hide for large screens when sidebar is closed
          }" @mouseenter="openSidebar" @mouseleave="handleMouseLeave">



          <div class="justify-end mb-4 flex">
            <div class="flex items-center gap-4 p-4
            ">
              <Checkbox inputId="size_normal" name="size" :value="true" v-model="isFixedSidebar" size="small"
                @change="toggleSidebar" />
            </div>
          </div>
          <div class="rounded-border flex-auto">
            <div class="p-4 font-medium text-2xl text-[#FFFFFF]" :class="{ hidden: activeTab2 !== 0 }">
              Dashboard

              <div v-show="activeTab2 === 0"
                class="flex-col justify-center text-sm my-10 transition-all duration-500 ease-in-out opacity-0"
                :class="{ 'opacity-100': activeTab2 === 0, 'opacity-0': activeTab2 !== 0, 'translate-y-0': activeTab2 === 0, 'translate-y-10': activeTab2 !== 0 }"
                style="animation: slideDown 0.5s ease-out forwards;">

                <div v-for="(item, index) in menuItems2" :key="index"
                  class="flex py-3 px-4 rounded-lg transition-colors duration-200 hover:scale-105 hover:bg-[#2F449D] hover:text-white"
                  :style="{ opacity: 0, animation: 'fadeIn ' + (0.5 + index * 0.2) + 's ease-out forwards, expandSize 0.5s ease-out forwards' }">

                  <span class="group">
                    <!-- Icon animation on hover -->
                    <svg v-if="item.icon" xmlns="http://www.w3.org/2000/svg" :width="item.icon.width"
                      :height="item.icon.height" :viewBox="item.icon.viewBox"
                      class="transition-transform duration-300 group-hover:animate-shake group-hover:scale-125">
                      <g v-for="(path, idx) in item.icon.paths" :key="idx" :fill="path.fill || 'none'"
                        :stroke="path.stroke || 'currentColor'" :stroke-linecap="path.strokeLinecap || 'round'"
                        :stroke-linejoin="path.strokeLinejoin || 'round'" :stroke-width="path.strokeWidth || 2">
                        <path :d="path.d" />
                      </g>
                    </svg>
                  </span>

                  <span class="px-2">
                    {{ item.name }}
                  </span>
                </div>



              </div>



            </div>
            <div class="p-4 font-medium text-2xl text-[#FFFFFF]" :class="{ hidden: activeTab2 !== 1 }">
              Bookmarks

              <div class=" flex justify-center text-xs  my-10
              ">


              </div>
            </div>
            <div class="p-4 font-medium text-2xl text-[#FFFFFF]" :class="{ hidden: activeTab2 !== 2 }">
              Team


              <div class=" flex justify-center text-xs  my-10
              ">


              </div>
            </div>
            <div class="p-4 font-medium text-2xl text-[#FFFFFF]" :class="{ hidden: activeTab2 !== 3 }">
              Messages

              <div class=" flex justify-center text-xs  my-10
              ">

              </div>
            </div>
            <div class="p-4 font-medium text-2xl text-[#FFFFFF]" :class="{ hidden: activeTab2 !== 4 }">
              Calendar

              <div class=" flex justify-center text-xs  my-10
              ">


              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="min-h-screen flex flex-col relative flex-auto"
      :class="isSidebarOpen || isFixedSidebar ? '' : 'w-[100%]'">
      <div
        class="h-[60px] flex justify-between lg:justify-start items-center px-8 bg-[#ffffff] border-b border-surface relative">
      </div>
      <div class="p-8 flex flex-col flex-auto">
        <div class="border-2 border-dashed rounded-border border-surface bg-[#ffffff] flex-auto p-5"
          :class="{ 'w-[calc(100%-5px)] ': isFixedSidebar, ' ml-20': !isFixedSidebar }">
          <Dashboard :client-name="clientName.value" :client-code="clientCode.value" />

        </div>
      </div>
    </div>
  </div>
</template>


<script setup>
import { ref, watch, onMounted } from 'vue';
import Checkbox from 'primevue/checkbox';
import 'primeicons/primeicons.css';
const activeTab2 = ref(0);
const isSidebarOpen = ref(false);
const isFixedSidebar = ref(false);

import { useRoute } from 'vue-router'; // Add this import
const clientName = ref('');
const clientCode = ref('');


const menuItems = [
  { icon: 'pi pi-home' },
  { icon: 'pi pi-bookmark' },
  { icon: 'pi pi-users' },
  { icon: 'pi pi-comments' },
  { icon: 'pi pi-calendar' },
];
const menuItems2 = [
  {
    name: 'Dashboard 1',
    icon: {
      width: 24,
      height: 24,
      viewBox: '0 0 24 24',
      paths: [
        { d: "M3 19.5v-15.5c0 -0.55 0.45 -1 1 -1h16c0.55 0 1 0.45 1 1v12c0 0.55 -0.45 1 -1 1h-14.5Z" },
        { d: "M8 7h8" },
        { d: "M8 10h8" },
        { d: "M8 13h4" },
      ]
    }
  },
  {
    name: 'Task',
    icon: {
      width: 24,
      height: 24,
      viewBox: '0 0 24 24',
      paths: [
        { d: "M9.813 15.904L9 18.75l-.813-2.846a4.5 4.5 0 0 0-3.09-3.09L2.25 12l2.846-.813a4.5 4.5 0 0 0 3.09-3.09L9 5.25l.813 2.846a4.5 4.5 0 0 0 3.09 3.09L15.75 12l-2.846.813a4.5 4.5 0 0 0-3.09 3.09ZM18.259 8.715 18 9.75l-.259-1.035a3.375 3.375 0 0 0-2.455-2.456L14.25 6l1.036-.259a3.375 3.375 0 0 0 2.455-2.456L18 2.25l.259 1.035a3.375 3.375 0 0 0 2.456 2.456L21.75 6l-1.035.259a3.375 3.375 0 0 0-2.456 2.456ZM16.894 20.567 16.5 21.75l-.394-1.183a2.25 2.25 0 0 0-1.423-1.423L13.5 18.75l1.183-.394a2.25 2.25 0 0 0 1.423-1.423l.394-1.183.394 1.183a2.25 2.25 0 0 0 1.423 1.423l1.183.394-1.183.394a2.25 2.25 0 0 0-1.423 1.423Z" }
      ]
    }
  },
  {
    name: 'New',
    icon: {
      width: 24,
      height: 24,
      viewBox: '0 0 24 24',
      paths: [
        { d: "M12 7.5h1.5m-1.5 3h1.5m-7.5 3h7.5m-7.5 3h7.5m3-9h3.375c.621 0 1.125.504 1.125 1.125V18a2.25 2.25 0 0 1-2.25 2.25M16.5 7.5V18a2.25 2.25 0 0 0 2.25 2.25M16.5 7.5V4.875c0-.621-.504-1.125-1.125-1.125H4.125C3.504 3.75 3 4.254 3 4.875V18a2.25 2.25 0 0 0 2.25 2.25h13.5M6 7.5h3v3H6v-3Z" }
      ]
    }
  },
  {
    name: 'Files',
    icon: {
      width: 24,
      height: 24,
      viewBox: '0 0 24 24',
      paths: [
        { d: "M3.75 9.776c.112-.017.227-.026.344-.026h15.812c.117 0 .232.009.344.026m-16.5 0a2.25 2.25 0 0 0-1.883 2.542l.857 6a2.25 2.25 0 0 0 2.227 1.932H19.05a2.25 2.25 0 0 0 2.227-1.932l.857-6a2.25 2.25 0 0 0-1.883-2.542m-16.5 0V6A2.25 2.25 0 0 1 6 3.75h3.879a1.5 1.5 0 0 1 1.06.44l2.122 2.12a1.5 1.5 0 0 0 1.06.44H18A2.25 2.25 0 0 1 20.25 9v.776" }
      ]
    }
  }
]
  ;


const toggleSidebar = () => {
  debugger
  if (isFixedSidebar.value) {
    isSidebarOpen.value = true;
  } else {
    isSidebarOpen.value = false;
  }
};



const openSidebar = () => {
  if (!isFixedSidebar.value) {
    isSidebarOpen.value = true;
  }
};


const handleMouseLeave = (event) => {
  const sidebar = document.getElementById('app-sidebar-10');
  const isOutside = !sidebar.contains(event.relatedTarget);
  if (isOutside && !isFixedSidebar.value) {
    isSidebarOpen.value = false;
  }
};

const changeActiveTab = (index) => {
  activeTab2.value = index;
};


watch(isFixedSidebar, (newValue) => {
  if (Array.isArray(newValue) && newValue.includes(true)) {
    isSidebarOpen.value = true;
  } else {
    isSidebarOpen.value = false;
    isFixedSidebar.value = false;
  }
});

onMounted(async () => {

  const route = useRoute();  // Access the current route
  // Get values from route params or set static values if not available
  clientName.value = route.query.clientName
    ? route.query.clientName
    : "";
  clientCode.value = route.query.clientCode
    ? route.query.clientCode
    : "";
  console.log(clientName.value, "clientName.value")


});


</script>

<style>
.hidden {
  transform: translateX(-100%);
}



.p-checkbox-checked .p-checkbox-box {
  border-color: #2F449D !important;
  background: #2F449D !important;
}

.p-menu-item .focus {
  border-color: #2F449D !important;
  background: #2F449D !important;
  color: #2F449D !important;

}



@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateX(-20px);
    /* Start from the left */
  }

  to {
    opacity: 1;
    transform: translateX(0);
    /* End at the original position */
  }
}

@keyframes fadeOut {
  from {
    opacity: 1;
    transform: translateX(0);
    /* Start at the original position */
  }

  to {
    opacity: 0;
    transform: translateX(-20px);
    /* Move to the left */
  }
}

.fade-in {
  animation: fadeIn 0.3s forwards;
  /* Adjust duration as needed */
}

.fade-out {
  animation: fadeOut 0.3s forwards;
  /* Adjust duration as needed */
}

/* Add this to your existing styles */
:root {
  font-family: 'Inter', sans-serif;
}

/* Or apply it specifically to your component */
#app-sidebar-10 {
  font-family: 'Inter', sans-serif;
}

@keyframes slideDown {
  0% {
    transform: translateY(-50px);
    opacity: 0;
  }

  100% {
    transform: translateY(0);
    opacity: 1;
  }
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}

@keyframes expandSize {
  from {
    transform: scale(0.9);
  }

  to {
    transform: scale(1);
  }
}
</style>