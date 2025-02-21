
<template>
    <div class="min-h-screen flex relative lg:static bg-gray-50">
        <div id="app-sidebar-1"
            class="bg-gray-0 h-screen hidden lg:block flex-shrink-0 absolute lg:static left-0 top-0 z-10 border-r border-gray select-none w-[280px]">
            <div class="flex flex-col h-full">
                <div class="flex items-center p-4 flex-shrink-0 h-[60px]">
                  <img src="@/public/images.jpg" alt="">
                 
                </div>
                <div class="overflow-y-auto">
                    <ul class="list-none p-4 m-0 bg-white">
                        <li>
                            <div v-styleclass="{
                                selector: '@next',
                                enterFromClass: 'hidden',
                                enterActiveClass: 'animate-slidedown',
                                leaveToClass: 'hidden',
                                leaveActiveClass: 'animate-slideup'
                            }"
                                class="p-4 flex items-center justify-between text-gray-600  cursor-pointer">
                                <span class="font-medium">FAVORITES</span>
                                <i class="pi pi-chevron-down" />
                            </div>
                            <ul class="list-none p-0 m-0 overflow-hidden">
                                <li>
                                    <a @click="setSelectedItem('dashboard')"
                                        class="flex items-center cursor-pointer p-4 rounded-border text-gray-700  hover:bg-gray-100  duration-150 transition-colors">
                                        <!-- <i class="pi pi-home mr-2 !text-xl !leading-none" /> -->
                                        <img src="@/public/home1.gif" alt="" height="30" width="30">
                                        <span class="font-medium">Dashboard</span>
                                    </a>
                                </li>
                                <li>
                                    <a @click="setSelectedItem('bookmarks')"
                                        class="flex items-center cursor-pointer p-4 rounded-border text-gray-700  hover:bg-gray-100  duration-150 transition-colors">
                                        <i class="pi pi-bookmark mr-2 !text-xl !leading-none" />
                                        <span class="font-medium">Bookmarks</span>
                                    </a>
                                </li>

                                <li>
                                    <a
                                        class="flex items-center cursor-pointer p-4 rounded-border text-gray-700  hover:bg-gray-100  duration-150 transition-colors">
                                        <i class="pi pi-users mr-2 !text-xl !leading-none" />
                                        <span class="font-medium">Team</span>
                                    </a>
                                </li>
                                <li>
                                    <a
                                        class="flex items-center cursor-pointer p-4 rounded-border text-gray-700  hover:bg-gray-100  duration-150 transition-colors">
                                        <i class="pi pi-comments mr-2 !text-xl !leading-none" />
                                        <span class="font-medium">Messages</span>
                                        <span
                                            class="inline-flex items-center justify-center ml-auto bg-primary text-primary-contrast  rounded-full min-w-6 h-6">3</span>
                                    </a>
                                </li>
                                <li>
                                    <a
                                        class="flex items-center cursor-pointer p-4 rounded-border text-gray-700  hover:bg-gray-100  duration-150 transition-colors">
                                        <i class="pi pi-calendar mr-2 !text-xl !leading-none" />
                                        <span class="font-medium">Calendar</span>
                                    </a>
                                </li>
                                <li>
                                    <a
                                        class="flex items-center cursor-pointer p-4 rounded-border text-gray-700  hover:bg-gray-100  duration-150 transition-colors">
                                        <i class="pi pi-cog mr-2 !text-xl !leading-none" />
                                        <span class="font-medium">Settings</span>
                                    </a>
                                </li>
                            </ul>
                        </li>
                    </ul>
                    <ul class="list-none p-4 m-0">
                        <li>
                            <div v-styleclass="{
                                selector: '@next',
                                enterFromClass: 'hidden',
                                enterActiveClass: 'animate-slidedown',
                                leaveToClass: 'hidden',
                                leaveActiveClass: 'animate-slideup'
                            }"
                                class="p-4 flex items-center justify-between text-gray-600  cursor-pointer">
                                <span class="font-medium">APPLICATION</span>
                                <i class="pi pi-chevron-down" />
                            </div>
                            <ul class="list-none p-0 m-0 overflow-hidden">
                                <li>
                                    <a
                                        class="flex items-center cursor-pointer p-4 rounded-border text-gray-700  hover:bg-gray-100  duration-150 transition-colors">
                                        <i class="pi pi-folder mr-2 !text-xl !leading-none" />
                                        <span class="font-medium">Projects</span>
                                    </a>
                                </li>
                                <li>
                                    <a
                                        class="flex items-center cursor-pointer p-4 rounded-border text-gray-700  hover:bg-gray-100  duration-150 transition-colors">
                                        <i class="pi pi-chart-bar mr-2 !text-xl !leading-none" />
                                        <span class="font-medium">Performance</span>
                                    </a>
                                </li>
                                <li>
                                    <a
                                        class="flex items-center cursor-pointer p-4 rounded-border text-gray-700  hover:bg-gray-100  duration-150 transition-colors">
                                        <i class="pi pi-cog mr-2 !text-xl !leading-none" />
                                        <span class="font-medium">Settings</span>
                                    </a>
                                </li>
                            </ul>
                        </li>
                    </ul>
                </div>
                <div class="mt-auto">
                    <hr class="mb-4 mx-4 border-t border-0 border-gray" />
                    <a
                        class="m-4 flex items-center cursor-pointer p-4 rounded-border text-gray-700  hover:bg-gray-100  duration-150 transition-colors">
                        <img src="https://fqjltiegiezfetthbags.supabase.co/storage/v1/render/image/public/block.images/blocks/avatars/circle/avatar-f-1.png"
                            class="mr-2 w-8 h-7" />
                        <span class="font-medium">Amy Elsner</span>
                    </a>
                </div>
            </div>
        </div>
        <div class="min-h-screen flex flex-col relative flex-auto">
            <div
                class="flex justify-between items-center px-8 bg-gray-0  border-b border-gray relative lg:static h-[60px]">
                <div class="flex">
                    <a v-styleclass="{
                        selector: '#app-sidebar-1',
                        enterFromClass: 'hidden',
                        enterActiveClass: 'animate-fadeinleft',
                        leaveToClass: 'hidden',
                        leaveActiveClass: 'animate-fadeoutleft',
                        hideOnOutsideClick: true
                    }" class="cursor-pointer block lg:hidden text-gray-700  mr-4 mt-1">
                        <i class="pi pi-bars text-4xl" />
                    </a>
                    <IconField icon-position="left">
                        <InputIcon class="pi pi-search text-gray-700" />
                        <InputText type="text" class="border-0 w-40 sm:w-80" placeholder="Search" />
                    </IconField>
                </div>
                <a v-styleclass="{
                    selector: '@next',
                    enterFromClass: 'hidden',
                    enterActiveClass: 'animate-fadein',
                    leaveToClass: 'hidden',
                    leaveActiveClass: 'animate-fadeout',
                    hideOnOutsideClick: true
                }" class="cursor-pointer block lg:hidden text-gray-700">
                    <i class="pi pi-ellipsis-v text-2xl" />
                </a>
                <ul
                    class="list-none p-0 m-0 hidden lg:flex lg:items-center select-none lg:flex-row border lg:border-0 border-gray right-0 top-full z-10 shadow lg:shadow-none absolute lg:static bg-gray-0">
                    <li>
                        <a
                            class="flex p-4 lg:px-4 lg:py-2 items-center text-gray-600  hover:text-gray-900  hover:bg-gray-100  font-medium rounded-border cursor-pointer duration-150 transition-colors">
                            <i class="pi pi-inbox text-base lg:!text-2xl leading-none mr-2 lg:mr-0" />
                            <span class="block lg:hidden font-medium">Inbox</span>
                        </a>
                    </li>
                    <li>
                        <a
                            class="flex p-4 lg:px-4 lg:py-2 items-center text-gray-600  hover:text-gray-900  hover:bg-gray-100  font-medium rounded-border cursor-pointer duration-150 transition-colors">
                            <OverlayBadge severity="danger" class="mr-2 lg:mr-0">
                                <i class="pi pi-bell text-base lg:!text-2xl leading-none" />
                            </OverlayBadge>
                            <span class="block lg:hidden font-medium">Notifications</span>
                        </a>
                    </li>
                    <li class="border-t border-gray lg:border-t-0">
                        <a
                            class="flex p-4 lg:px-4 lg:py-2 items-center hover:bg-gray-100  font-medium rounded-border cursor-pointer duration-150 transition-colors">
                            <img src="https://fqjltiegiezfetthbags.supabase.co/storage/v1/render/image/public/block.images/blocks/avatars/circle/avatar-f-1.png"
                                class="mr-4 lg:mr-0 w-8 h-8" />
                            <div class="block lg:hidden">
                                <div class="text-gray-900  font-medium">Josephine Lillard</div>
                                <span class="text-gray-600  font-medium text-sm">Marketing
                                    Specialist</span>
                            </div>
                        </a>
                    </li>
                </ul>
            </div>
            <div class="p-8 flex flex-col flex-auto">
                <div
                    class=" my-10 bg-gray-0  flex-auto">
                    <div v-if="selectedItem === 'dashboard'">
                        <Dashboard />
                    </div>
                    <div v-if="selectedItem === 'bookmarks'">2 value</div>
                    <div v-if="selectedItem === 'reports'">3 value</div>
                    <div v-if="selectedItem === 'team'">4 value</div>
                    <div v-if="selectedItem === 'messages'">5 value</div>
                </div>
            </div>
        </div>

    </div>
</template>
<script setup>
import IconField from 'primevue/iconfield';
import InputIcon from 'primevue/inputicon';
import InputText from 'primevue/inputtext';
import OverlayBadge from 'primevue/overlaybadge';
import 'primeicons/primeicons.css';
import Dashboard from './components/Dashboard.vue';
const selectedItem = ref('dashboard');


const setSelectedItem = (item) => {
    selectedItem.value = item;
};
</script>
