<template>
  <div
    :class="isSidebarOpen || isFixedSidebar ? 'min-h-screen flex relative lg:static bg-[#f8fafc]' : 'min-h-screen flex relative lg:static bg-[#f8fafc]'">
    <div id="app-sidebar-10"
      class="h-full lg:h-auto flex-shrink-0 left-0 top-0 z-20 border-r border-surface transition-all duration-300"
      :class="isFixedSidebar ? 'w-[300px]' : 'w-0'" @mouseenter="openSidebar" @mouseleave="handleMouseLeave">
      <div class="flex h-full">
        <div class="flex flex-col h-full bg-[#FFFFFF] flex-shrink-0 select-none border-r-2 border-dotted">
          <div class="flex items-center justify-between flex-shrink-0 h-[60px] mx-5">
            <div class="flex items-center justify-center">
              <svg height="36" viewBox="0 0 48 50" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" clip-rule="evenodd"
                  d="M33.1548 9.65956L23.9913 4.86169L5.54723 14.5106L0.924465 12.0851L23.9913 0L37.801 7.23403L33.1548 9.65956ZM23.9931 19.3085L42.4255 9.65955L47.0717 12.0851L23.9931 24.1595L10.1952 16.9361L14.8297 14.5106L23.9931 19.3085ZM4.6345 25.8937L0 23.4681V37.9149L23.0669 50V45.1489L4.6345 35.4894V25.8937ZM18.4324 28.2658L0 18.6169V13.7658L23.0669 25.8403V40.2977L18.4324 37.8615V28.2658ZM38.7301 23.468V18.6169L24.9205 25.8403V49.9999L29.555 47.5743V28.2659L38.7301 23.468ZM43.3546 35.4892V16.1914L48.0008 13.7659V37.9148L34.1912 45.1488V40.2977L43.3546 35.4892Z"
                  class="fill-[#6b58a8]" />
              </svg>
            </div>
          </div>
          <div class="overflow-y-auto mt-4">
            <ul class="list-none py-4 px-2 m-0">
              <li class="mb-2" v-for="(item, index) in menuItems" :key="index">
                <a class="rounded-md flex items-center cursor-pointer   px-2 justify-center text-[#B29AFD] duration-150 transition-colors  "
                  :class="{ '': activeTab2 === index }" @click="activeTab2 = index"
                  @mouseenter="changeActiveTab(index)"       
              




                  >
                       <!-- v-tooltip="{ value: item.name, autoHide: false }" -->               
                  <!-- Keep icon color consistent with text-[#FFFFFF] -->

                  <!-- <i :class="['text-xl', item.icon, 'text-[#FFFFFF]'

                    , { 'hover:text-gray-400': isSidebarOpen || isFixedSidebar }]" style="font-size: 1.5rem"></i> -->
                    <component :is="item.component" class="text-xl text-[#B29AFD] hover:bg-[#ebe8fa] p-2 rounded-md " :class="{ 'hover:text-gray-400': isSidebarOpen || isFixedSidebar }" style="font-size: 1.5rem"></component>

                </a>
              </li>
            </ul>
          </div>
          <div class="mt-auto">
            <hr class="mb-4 mx-2 border-t border-0 border-[#FFFFFF]/20" />
            <a
              class="m-4 flex items-center cursor-pointer p-2 justify-center hover:bg-[#dad5f2] rounded-border text-[#cbd5e1] hover:text-[#ffffff] duration-150 transition-colors">
              <img
                src="https://fqjltiegiezfetthbags.supabase.co/storage/v1/render/image/public/block.images/blocks/avatars /circle/avatar-f-1.png"
                class="w-6 h-6" />
            </a>
          </div>
        </div>
        <div
    id="app-sidebar-10"
    class="h-full lg:h-auto flex-shrink-0 left-0 top-0 z-20 border-r border-surface bg-[#fff] px-1 py-6"
    :class="{
      'w-[230px] opacity-100 fade-in': isSidebarOpen || isFixedSidebar, // When open, full width and fully visible
      'w-0 opacity-0 fade-out delay-150': !isSidebarOpen && !isFixedSidebar, // When closed, zero width and fully transparent
      'transition-all duration-500 ease-in-out': isSidebarOpen || isFixedSidebar, // 0.5-second smooth transition for all properties
      'lg:block': isFixedSidebar || isSidebarOpen, // Show for large screens when sidebar is open
      'lg:hidden': !isFixedSidebar && !isSidebarOpen // Hide for large screens when sidebar is closed
    }"
    @mouseenter="openSidebar" 
    @mouseleave="handleMouseLeave"
  >


          <div class="justify-end  flex justify-between px-4 ">
            <div>
              <div v-if=" activeTab2 === 0" class=" font-semibold text-lg text-[#484e59]"> Dashboard</div>
              <div v-if=" activeTab2 === 1"  class=" font-semibold text-lg text-[#484e59]"> Bookmarks</div>
              <div v-if=" activeTab2 === 2"  class=" font-semibold text-lg text-[#484e59]"> Team</div>
              <div v-if=" activeTab2 === 3"  class=" font-semibold text-lg text-[#484e59]"> Messages</div>
              <div v-if=" activeTab2 === 4"  class=" font-semibold text-lg text-[#484e59]"> Calender</div>
            </div>
          
            <div class="flex items-center
            ">
              <Checkbox inputId="size_normal" name="size" :value="true" v-model="isFixedSidebar" size="small"
                @change="toggleSidebar" />
            </div>
         
          </div>
          <div class="rounded-border flex-auto cols-span-10">
            <div class="px-4 font-semibold text-lg text-[#484e59]" :class="{ hidden: activeTab2 !== 0 }">
              <!-- Dashboard -->
              <div v-show="activeTab2 === 0"
    class="flex-col justify-center text-sm my-5 transition-all duration-500 ease-in-out opacity-0"
    :class="{ 'opacity-100': activeTab2 === 0, 'opacity-0': activeTab2 !== 0, 'translate-y-0': activeTab2 === 0, 'translate-y-10': activeTab2 !== 0 }"
    style="animation: slideDown 0.5s ease-out forwards;">

    <div v-for="(item, index) in menuItems2" :key="index"
      class="flex py-3 px-4 rounded-lg duration-200 hover:scale-105 text-[#4b4d59] custom font-sans hover:bg-[#b49ef7] hover:text-[#fff]"
      :style="{ opacity: 0, animation: 'fadeIn ' + (0.5 + index * 0.2) + 's ease-out forwards, expandSize 0.5s ease-out forwards' }">

      <span class="group">
        <!-- Icon rendering -->
        <div v-html="item.icon"></div>
      </span>

      <!-- Menu Item Name -->
      <span class="px-2">
        {{ item.name }}
      </span>
    </div>
  </div>



            </div>
            <div class=" px-4 font-semibold text-lg text-[#484e59]" :class="{ hidden: activeTab2 !== 1 }">
              <!-- Bookmarks -->

              <div v-show="activeTab2 === 1"
    class="flex-col justify-center text-sm my-5 transition-all duration-500 ease-in-out opacity-0"
    :class="{ 'opacity-100': activeTab2 === 0, 'opacity-0': activeTab2 !== 0, 'translate-y-0': activeTab2 === 0, 'translate-y-10': activeTab2 !== 0 }"
    style="animation: slideDown 0.5s ease-out forwards;">

    <div v-for="(item, index) in menuItems3" :key="index"
      class="flex py-3 px-4 rounded-lg duration-200 hover:scale-105  text-[#4b4d59] custom font-sans hover:bg-[#b49ef7] hover:text-[#fff] "
      :style="{ opacity: 0, animation: 'fadeIn ' + (0.5 + index * 0.2) + 's ease-out forwards, expandSize 0.5s ease-out forwards' }">

      <span class="group">
        <!-- Icon rendering -->
        <div v-html="item.icon"></div>
      </span>

      <!-- Menu Item Name -->
      <span class="px-2">
        {{ item.name }}
      </span>
    </div>
  </div>

            </div>
            <div class=" px-4 font-semibold text-lg text-[#484e59]" :class="{ hidden: activeTab2 !== 2 }">
              <!-- Team -->


           
              <div v-show="activeTab2 === 2"
                class="flex-col justify-center text-sm my-10 transition-all duration-500 ease-in-out opacity-0"
                :class="{ 'opacity-100': activeTab2 === 0, 'opacity-0': activeTab2 !== 0, 'translate-y-0': activeTab2 === 0, 'translate-y-10': activeTab2 !== 0 }"
                style="animation: slideDown 0.5s ease-out forwards;">

                <div v-for="(item, index) in menuItems4" :key="index"
                  class="flex py-3 px-4 rounded-lg  duration-200 hover:scale-105  text-gray-400 hover:bg-[#b49ef7] hover:text-[#fff]"
                  :style="{ opacity: 0, animation: 'fadeIn ' + (0.5 + index * 0.2) + 's ease-out forwards, expandSize 0.5s ease-out forwards' }">

                  <!-- <span class="group">
                   
                    <svg v-if="item.icon" xmlns="http://www.w3.org/2000/svg" :width="item.icon.width"
                      :height="item.icon.height" :viewBox="item.icon.viewBox"
                      class="transition-transform duration-300 
                       ">
                      <g v-for="(path, idx) in item.icon.paths" :key="idx" :fill="path.fill || 'none'"
                        :stroke="path.stroke || 'currentColor'" :stroke-linecap="path.strokeLinecap || 'round'"
                        :stroke-linejoin="path.strokeLinejoin || 'round'" :stroke-width="path.strokeWidth || 2">
                        <path :d="path.d" />
                      </g>
                    </svg>
                  </span> -->
                  <span class="inline-flex items-center   flex-grow-0"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20" class=" h-5 w-5"><g fill="currentColor" clip-path="url(#graph_svg__clip0_4314_12611)"><path d="M2.174 19.153c-.697-.017-1.225-.437-1.282-1.132a22 22 0 0 1-.059-1.771c0-.784.025-1.356.06-1.772.056-.695.584-1.114 1.281-1.132.305-.008.687-.013 1.16-.013s.853.005 1.158.013c.697.018 1.225.437 1.282 1.132.034.416.06.989.06 1.772s-.026 1.355-.06 1.771c-.057.695-.585 1.115-1.282 1.132-.305.008-.686.013-1.159.013-.472 0-.854-.005-1.159-.013M15.704 19.15c-.812-.033-1.381-.604-1.434-1.415-.054-.84-.104-2.207-.104-4.402 0-2.194.05-3.56.104-4.402.053-.81.622-1.382 1.434-1.414q.4-.016.962-.017.563.001.963.017c.812.032 1.381.603 1.434 1.414.055.842.104 2.208.104 4.402s-.05 3.561-.104 4.402c-.053.811-.622 1.382-1.434 1.414q-.4.017-.963.018-.561 0-.962-.018M8.98 19.152c-.778-.023-1.345-.534-1.4-1.31A41 41 0 0 1 7.5 15c0-1.328.035-2.232.08-2.842.055-.777.622-1.287 1.4-1.31a33.672 33.672 0 0 1 2.039 0c.779.023 1.346.533 1.402 1.31.044.61.079 1.514.079 2.842s-.035 2.23-.08 2.841c-.055.777-.622 1.288-1.4 1.311-.28.009-.617.014-1.02.014s-.74-.005-1.02-.014" opacity="0.35"></path><path d="M17.467 5.042c-.042.824-.825 1.133-1.432.576a47 47 0 0 1-1-.949 536 536 0 0 0-3.91 3.595c-.431.4-1.132.356-1.509-.096A96 96 0 0 0 7.36 5.543a37 37 0 0 0-4.124 3.528 1.042 1.042 0 0 1-1.473-1.474C3.338 6.023 5.066 4.546 6.92 3.303l.003-.002a1.04 1.04 0 0 1 1.314.13c.807.806 1.536 1.694 2.274 2.563a530 530 0 0 1 3.052-2.8 45 45 0 0 1-.845-.895c-.558-.607-.248-1.39.575-1.432 1.05-.053 2.13-.084 3.167.11.468.088.81.43.898.898.194 1.038.163 2.117.11 3.167"></path></g></svg></span>

                  <span class="px-2">
                    {{ item.name }}
                  </span>
                </div>
                



              </div>
            </div>
            <div class=" px-4 font-semibold text-lg text-[#484e59]" :class="{ hidden: activeTab2 !== 3 }">
              <!-- Messages -->

              <div class=" flex justify-center text-xs  my-10
              ">

              </div>
            </div>
            <div class=" px-4 font-semibold text-lg text-[#484e59]" :class="{ hidden: activeTab2 !== 4 }">
              <!-- Calendar -->

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
import ChatIcon from './components/ChatIcon.vue';
import BookmarkIcon from './components/BookmarkIcon.vue';
import CalenderIcon from './components/CalenderIcon.vue';
import UserIcon from './components/UserIcon.vue';
import CommentsIcon from './components/CommentsIcon.vue';

import Tooltip from 'primevue/tooltip';



const activeTab2 = ref(0);
const isSidebarOpen = ref(false);
const isFixedSidebar = ref(false);

import { useRoute } from 'vue-router'; // Add this import
const clientName = ref('');
const clientCode = ref('');


const menuItems = [
  { component: ChatIcon,name:'Dashboard' }, // Chat icon component
  { component: BookmarkIcon,name:"Bookmarks" }, 
  { component: UserIcon ,name:"Team"},
  { component: CommentsIcon,name:"Messages" },
  { component: CalenderIcon,name:"Calender" },  // Bookmark icon component
  // Add other icons similarly
];
const menuItems2 = [
  {
    name: 'Analitics',
    icon: '<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20" class=" h-5 w-5"><g fill="currentColor" clip-path="url(#graph_svg__clip0_4314_12611)"><path d="M2.174 19.153c-.697-.017-1.225-.437-1.282-1.132a22 22 0 0 1-.059-1.771c0-.784.025-1.356.06-1.772.056-.695.584-1.114 1.281-1.132.305-.008.687-.013 1.16-.013s.853.005 1.158.013c.697.018 1.225.437 1.282 1.132.034.416.06.989.06 1.772s-.026 1.355-.06 1.771c-.057.695-.585 1.115-1.282 1.132-.305.008-.686.013-1.159.013-.472 0-.854-.005-1.159-.013M15.704 19.15c-.812-.033-1.381-.604-1.434-1.415-.054-.84-.104-2.207-.104-4.402 0-2.194.05-3.56.104-4.402.053-.81.622-1.382 1.434-1.414q.4-.016.962-.017.563.001.963.017c.812.032 1.381.603 1.434 1.414.055.842.104 2.208.104 4.402s-.05 3.561-.104 4.402c-.053.811-.622 1.382-1.434 1.414q-.4.017-.963.018-.561 0-.962-.018M8.98 19.152c-.778-.023-1.345-.534-1.4-1.31A41 41 0 0 1 7.5 15c0-1.328.035-2.232.08-2.842.055-.777.622-1.287 1.4-1.31a33.672 33.672 0 0 1 2.039 0c.779.023 1.346.533 1.402 1.31.044.61.079 1.514.079 2.842s-.035 2.23-.08 2.841c-.055.777-.622 1.288-1.4 1.311-.28.009-.617.014-1.02.014s-.74-.005-1.02-.014" opacity="0.35"></path><path d="M17.467 5.042c-.042.824-.825 1.133-1.432.576a47 47 0 0 1-1-.949 536 536 0 0 0-3.91 3.595c-.431.4-1.132.356-1.509-.096A96 96 0 0 0 7.36 5.543a37 37 0 0 0-4.124 3.528 1.042 1.042 0 0 1-1.473-1.474C3.338 6.023 5.066 4.546 6.92 3.303l.003-.002a1.04 1.04 0 0 1 1.314.13c.807.806 1.536 1.694 2.274 2.563a530 530 0 0 1 3.052-2.8 45 45 0 0 1-.845-.895c-.558-.607-.248-1.39.575-1.432 1.05-.053 2.13-.084 3.167.11.468.088.81.43.898.898.194 1.038.163 2.117.11 3.167"></path></g></svg>'
  },
  {
    name: 'Ecommerce',
    icon:'<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20" class=" h-5 w-5"><path fill="currentColor" d="M2.842 1.667a1.042 1.042 0 0 0 0 2.083h.702c.197 0 .368.139.408.332.186.891.713 3.384 1.135 5.085a58 58 0 0 0 1.294 4.502 2.501 2.501 0 0 1 3.594 1.286c.623.028 1.35.045 2.195.045.715 0 1.333-.012 1.868-.033a2.5 2.5 0 0 1 3.611-1.29c.294-.741.69-1.982 1.026-3.885.24-1.365.389-2.39.48-3.133C19.267 5.745 18.554 5 17.633 5H6.383l-.517-2.07a1.67 1.67 0 0 0-1.617-1.263z" opacity="0.32"></path><path fill="currentColor" d="M14.625 8.829a.83.83 0 1 0-1.65-.165l-.25 2.508a.83.83 0 1 0 1.65.165zM10.625 8.664a.83.83 0 1 0-1.65.165l.25 2.508a.83.83 0 1 0 1.65-.165zM13.884 15.833a2.5 2.5 0 1 0 5 0 2.5 2.5 0 0 0-5 0M5.134 15.833a2.5 2.5 0 1 0 5 0 2.5 2.5 0 0 0-5 0"></path></svg>'
  },
  {
    name: 'Business',
    icon: '<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20" class=" h-5 w-5"><path fill="currentColor" d="M16.667 6.875V15c0 2.5-1.492 3.334-3.334 3.334H6.667c-1.842 0-3.334-.834-3.334-3.334V6.875c0-2.708 1.492-3.333 3.334-3.333 0 .517.208.983.55 1.325.341.342.808.55 1.325.55h2.916a1.88 1.88 0 0 0 1.875-1.875c1.842 0 3.334.625 3.334 3.333" opacity="0.35"></path><path fill="currentColor" d="M13.333 3.542a1.88 1.88 0 0 1-1.875 1.875H8.542c-.517 0-.984-.208-1.325-.55a1.86 1.86 0 0 1-.55-1.325c0-1.033.841-1.875 1.875-1.875h2.916c.517 0 .984.208 1.325.55.342.342.55.808.55 1.325M10 11.458H6.667a.63.63 0 0 1-.625-.625.63.63 0 0 1 .625-.625H10a.63.63 0 0 1 .625.625.63.63 0 0 1-.625.625M13.333 14.792H6.667a.63.63 0 0 1-.625-.625.63.63 0 0 1 .625-.625h6.666a.63.63 0 0 1 .625.625.63.63 0 0 1-.625.625"></path></svg>'
  },

]
  ;
  const menuItems3 = [
  {
    name: 'Home',
    icon: '<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20" class=" h-5 w-5"><path fill="currentColor" fill-rule="evenodd" d="M3.436 1.87c.995-.102 2.651-.203 5.314-.203s4.319.1 5.314.203c.85.088 1.47.718 1.567 1.567.102.886.202 2.224.202 4.063 0 1.84-.1 3.177-.202 4.063-.098.85-.716 1.48-1.567 1.568-.879.09-2.273.18-4.421.199a1.26 1.26 0 0 0-.887.373l-1.41 1.43c-.611.62-1.669.26-1.775-.605l-.111-.91a.42.42 0 0 0-.397-.367 33 33 0 0 1-1.626-.12c-.85-.088-1.47-.719-1.568-1.568-.102-.886-.202-2.224-.202-4.063s.1-3.177.202-4.063c.098-.849.717-1.48 1.567-1.567M5.833 5a.833.833 0 1 0 0 1.667h5.834a.833.833 0 1 0 0-1.667zm0 3.75a.833.833 0 1 0 0 1.667h3.334a.833.833 0 1 0 0-1.667z" clip-rule="evenodd" opacity="0.35"></path><path fill="currentColor" d="M5 5.833c0-.46.372-.833.833-.833h5.833a.833.833 0 0 1 0 1.667H5.833a.833.833 0 0 1-.834-.834M5 9.583c0-.46.372-.833.833-.833h3.333a.833.833 0 1 1 0 1.667H5.833a.833.833 0 0 1-.834-.834M8.355 14.11l.4-.406c.234-.238.554-.371.887-.374 2.148-.02 3.543-.109 4.422-.2.85-.087 1.469-.718 1.566-1.567.067-.578.133-1.35.17-2.329.423.025.756.055 1.015.084.52.059.903.435.968.956.068.544.133 1.393.133 2.643s-.065 2.1-.133 2.643c-.065.521-.448.897-.969.956-.348.04-.83.079-1.484.108a.42.42 0 0 0-.394.337l-.143.722a.625.625 0 0 1-1.026.348l-1.207-1.065a1.27 1.27 0 0 0-.81-.314 27 27 0 0 1-2.315-.136 1.07 1.07 0 0 1-.969-.955 17 17 0 0 1-.111-1.452"></path></svg>'
  },
  {
    name: 'Messages',
    icon: '<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20" class=" h-5 w-5"><path fill="currentColor" d="M3.333 8.296V4.167a2.5 2.5 0 0 1 2.5-2.5h8.334a2.5 2.5 0 0 1 2.5 2.5v4.13c0 .545-.266 1.055-.722 1.354-1.41.924-4.52 2.85-5.945 2.85s-4.535-1.926-5.945-2.85a1.61 1.61 0 0 1-.722-1.355" opacity="0.35"></path><path fill="currentColor" d="M3.333 5.209c-.425.315-.8.603-1.101.839-.502.392-.816.97-.859 1.606-.058.865-.124 2.316-.124 4.43 0 1.997.119 3.404.23 4.282.09.724.575 1.298 1.29 1.446 1.146.237 3.334.521 7.23.521s6.085-.284 7.23-.521c.716-.148 1.2-.722 1.291-1.446.111-.878.23-2.285.23-4.283 0-2.113-.067-3.564-.125-4.429a2.23 2.23 0 0 0-.858-1.606 56 56 0 0 0-1.101-.839v3.087c0 .545-.265 1.055-.722 1.354-1.41.925-4.52 2.85-5.945 2.85s-4.534-1.925-5.945-2.85a1.61 1.61 0 0 1-.721-1.354z"></path><path fill="currentColor" d="M5.833 4.792c0-.345.28-.625.625-.625h3.75a.625.625 0 1 1 0 1.25h-3.75a.625.625 0 0 1-.625-.625M5.833 7.708c0-.345.28-.625.625-.625h6.25a.625.625 0 1 1 0 1.25h-6.25a.625.625 0 0 1-.625-.625"></path></svg>'
  },
  {
    name: 'Notifications',
    icon: '<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20" class=" h-5 w-5"><path fill="currentColor" d="M18.333 8.75c0 2.255-.06 4.022-.117 5.168-.038.781-.794 1.341-1.568 1.237-1.27-.171-3.415-.363-6.648-.363s-5.377.192-6.648.363c-.774.104-1.53-.456-1.568-1.237a107 107 0 0 1-.117-5.168c0-2.255.06-4.021.117-5.168.038-.78.794-1.34 1.568-1.236 1.27.17 3.416.363 6.648.363 3.233 0 5.378-.192 6.648-.363.774-.105 1.53.456 1.568 1.236.056 1.147.117 2.913.117 5.168" opacity="0.32"></path><path fill="currentColor" d="M4.659 15.008a27 27 0 0 0-.779 2.075c-.073.227.064.465.3.488.387.038.8.02 1.116-.007.345-.03.647-.227.834-.517.492-.762.969-1.556 1.352-2.213-1.123.04-2.059.103-2.823.174M12.518 14.834c.383.657.86 1.451 1.352 2.213.187.29.49.487.834.517a6.4 6.4 0 0 0 1.116.007c.237-.023.373-.262.3-.488a27 27 0 0 0-.779-2.075c-.764-.07-1.7-.134-2.823-.174"></path></svg>'
  },
  {
    name: 'Settings',
    icon: '<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20" class=" h-5 w-5"><path fill="currentColor" d="M16.667 6.875V15c0 2.5-1.492 3.334-3.334 3.334H6.667c-1.842 0-3.334-.834-3.334-3.334V6.875c0-2.708 1.492-3.333 3.334-3.333 0 .517.208.983.55 1.325.341.342.808.55 1.325.55h2.916a1.88 1.88 0 0 0 1.875-1.875c1.842 0 3.334.625 3.334 3.333" opacity="0.35"></path><path fill="currentColor" d="M13.333 3.542a1.88 1.88 0 0 1-1.875 1.875H8.542c-.517 0-.984-.208-1.325-.55a1.86 1.86 0 0 1-.55-1.325c0-1.033.841-1.875 1.875-1.875h2.916c.517 0 .984.208 1.325.55.342.342.55.808.55 1.325M10 11.458H6.667a.63.63 0 0 1-.625-.625.63.63 0 0 1 .625-.625H10a.63.63 0 0 1 .625.625.63.63 0 0 1-.625.625M13.333 14.792H6.667a.63.63 0 0 1-.625-.625.63.63 0 0 1 .625-.625h6.666a.63.63 0 0 1 .625.625.63.63 0 0 1-.625.625"></path></svg>'
  }
];

const menuItems4 = [
  {
    name: 'Dashboard',
    icon: {
      width: 24,
      height: 24,
      viewBox: '0 0 24 24',
      paths: [
        { d: "M3 3h18v18H3z" },
        { d: "M3 9h18" },
        { d: "M9 3v18" }
      ]
    }
  },
  {
    name: 'Users',
    icon: {
      width: 24,
      height: 24,
      viewBox: '0 0 24 24',
      paths: [
        { d: "M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4s-4 1.79-4 4s1.79 4 4 4Z" },
        { d: "M8 14c-1.11 0-2 .89-2 2s.89 2 2 2h8c1.11 0 2-.89 2-2s-.89-2-2-2H8Z" }
      ]
    }
  },
  {
    name: 'Calendar',
    icon: {
      width: 24,
      height: 24,
      viewBox: '0 0 24 24',
      paths: [
        { d: "M3 5h18V3h-2V1h-2v2h-8V1h-2v2H3z" },
        { d: "M3 7h18v14H3z" },
        { d: "M3 7v14h18V7" }
      ]
    }
  },
  {
    name: 'Reports',
    icon: {
      width: 24,
      height: 24,
      viewBox: '0 0 24 24',
      paths: [
        { d: "M5 3h14v18H5z" },
        { d: "M5 7h14" },
        { d: "M5 11h14" },
        { d: "M5 15h14" }
      ]
    }
  }
];


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

* {
  font-family: 'Inter', sans-serif; /* Add your custom font here */
}


.hidden {
  transform: translateX(-100%);
}



.p-checkbox-checked .p-checkbox-box {
  border-color: #6b58a8 !important;
  background: #6b58a8 !important;
}

.p-menu-item .focus {
  border-color: #6b58a8 !important;
  background: #6b58a8 !important;
  color: #6b58a8 !important;

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
.custom{
  font-weight: 600;
  font-family: 'Inter',sans-serif;
}
</style>