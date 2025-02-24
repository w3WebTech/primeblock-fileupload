<template>
    <div :class="isSidebarOpen ? 'min-h-screen flex relative lg:static bg-[#f8fafc]' : 'min-h-screen flex relative lg:static bg-[#f8fafc]'">
        
        <div id="app-sidebar-10"
            class="h-full lg:h-auto flex-shrink-0 left-0 top-0 z-20 border-r border-surface w-full md:w-auto"
            @mouseenter="openSidebar" @mouseleave="handleMouseLeave">
            <div class="flex h-full">
                <div class="flex flex-col h-full bg-[#059669] flex-shrink-0 select-none">
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
                                <a class="rounded-l-full flex items-center cursor-pointer py-4 pl-0 pr-2 justify-center hover:bg-[#10B981] text-[#FFFFFF] duration-150 transition-colors"
                                    :class="{ 'bg-[#10B981]': activeTab2 === index }" @click="activeTab2 = index"
                                    @mouseenter="openSidebar">
                                    <i :class="item.icon + ' !text-xl'" ></i>
                                </a>
                            </li>
                        </ul>
                    </div>
                    <div class="mt-auto">
                        <hr class="mb-4 mx-2 border-t border-0 border-[#FFFFFF]/20" />
                        <a
                            class="m-4 flex items-center cursor-pointer p-2 justify-center hover:bg-[#10B981] rounded-border text-[#cbd5e1] hover:text-[#ffffff] duration-150 transition-colors">
                            <img src="https://fqjltiegiezfetthbags.supabase.co/storage/v1/render/image/public/block.images/blocks/avatars/circle/avatar-f-1.png"
                                class="w-6 h-6" />
                        </a>
                    </div>
                </div>
                <div class="flex flex-col bg-[#10B981] p-6 overflow-y-auto flex-shrink-0 grow md:grow-0 w-[300px]"
                    :class="{ 'hidden': !isSidebarOpen, 'absolute': !isSidebarOpen && !isFixedSidebar, 'lg:block': true }">
                    <div class="justify-end mb-4 flex">
                        <!-- <label class="inline-flex items-center cursor-pointer">
                            <input type="checkbox" class="form-checkbox" v-model="isFixedSidebar" />
                            <span class="ml-2 text-white">Fix Sidebar</span>
                        </label> -->
                        <div class="flex items-center gap-2">
        <Checkbox  inputId="size_normal" name="size" value="Normal" v-model="isFixedSidebar"  />
        
    </div>
                    </div>
                    <div class="rounded-border flex-auto">
                        <div class="p-4 font-medium text-2xl text-[#FFFFFF]" :class="{ hidden: activeTab2 !== 0 }">
                            Dashboard
                        </div>
                        <div class="p-4 font-medium text-2xl text-[#FFFFFF]" :class="{ hidden: activeTab2 !== 1 }">
                            Bookmarks
                        </div>
                        <div class="p-4 font-medium text-2xl text-[#FFFFFF]" :class="{ hidden: activeTab2 !== 2 }">Team
                        </div>
                        <div class="p-4 font-medium text-2xl text-[#FFFFFF]" :class="{ hidden: activeTab2 !== 3 }">
                            Messages
                        </div>
                        <div class="p-4 font-medium text-2xl text-[#FFFFFF]" :class="{ hidden: activeTab2 !== 4 }">
                            Calendar
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="min-h-screen flex flex-col relative flex-auto" :class="isSidebarOpen ? ' ' : 'w-[100%]'">
            <div
                class="h-[60px] flex justify-between lg:justify-start items-center px-8 bg-[#ffffff] border-b border-surface relative">
                <!-- <div class="flex">
                    <button @click="toggleSidebar" class="cursor-pointer block text-[#334155] mr-4 mt-1">
                        <i class="pi pi-bars text-2xl" />
                    </button>
                </div> -->
            </div>
            <div class="p-8 flex flex-col flex-auto">
                <div class="border-2 border-dashed rounded-border border-surface bg-[#ffffff] flex-auto p-5">
                    Test
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import OverlayBadge from 'primevue/overlaybadge';
import 'primeicons/primeicons.css';

const activeTab2 = ref(0);
const isSidebarOpen = ref(false); // Initially closed
const isFixedSidebar = ref(false);

const menuItems = [
    { icon: 'pi pi-home' },
    { icon: 'pi pi-bookmark' },
    { icon: 'pi pi-users' },
    { icon: 'pi pi-comments' },
    { icon: 'pi pi-calendar' },
];

const toggleSidebar = () => {
    if (!isFixedSidebar.value) {
        isSidebarOpen.value = !isSidebarOpen.value;
    }
};

const openSidebar = () => {
    if (!isFixedSidebar.value) {
        isSidebarOpen.value = true;
    }
};

const closeSidebar = () => {
    if (!isFixedSidebar.value) {
        isSidebarOpen.value = false;
    }
};

const handleMouseLeave = (event) => {
    const sidebar = document.getElementById('app-sidebar-10');
    const isOutside = !sidebar.contains(event.relatedTarget);
    if (isOutside) {
        closeSidebar();
    }
};
</script>

<style>
#app-sidebar-10 {
    transition: transform 0.3s ease;
}

.hidden {
    transform: translateX(-100%);
}
</style>