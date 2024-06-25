<template>

<header class="bg-white shadow">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex justify-between h-16">
      <div class="flex">
        <div class="flex-shrink-0 flex items-center">
          <img class="h-8 w-auto" src="/logo.png" alt="Your Company">
        </div>
      </div>
      <div class="-mr-2 flex items-center sm:hidden">
        <button type="button" class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-gray-500 hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500" aria-controls="mobile-menu" aria-expanded="false">
          <span class="sr-only">Open main menu</span>
          <svg class="h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          </svg>
        </button>
      </div>
      <div class="hidden sm:ml-6 sm:flex sm:space-x-8">
        <a href="#" class="inline-flex items-center px-1 pt-1 border-b-2 border-transparent text-sm font-medium text-gray-500 hover:border-gray-300 hover:text-gray-700">Home</a>
        <a href="#" class="inline-flex items-center px-1 pt-1 border-b-2 border-transparent text-sm font-medium text-gray-500 hover:border-gray-300 hover:text-gray-700">About</a>
        <a href="#" class="inline-flex items-center px-1 pt-1 border-b-2 border-transparent text-sm font-medium text-gray-500 hover:border-gray-300 hover:text-gray-700">Services</a>
        <a href="#" class="inline-flex items-center px-1 pt-1 border-b-2 border-transparent text-sm font-medium text-gray-500 hover:border-gray-300 hover:text-gray-700">Contact</a>
      </div>
    </div>
  </div>
</header>

  <Disclosure as="nav" v-slot="{ open }">
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
      <div class="relative flex h-16 items-center justify-between">
        <div class="absolute inset-y-0 right-0 flex items-center sm:hidden">
          <!-- Mobile menu button-->
          <DisclosureButton
            class="relative inline-flex items-center justify-center rounded-md p-2 text-gray-400 hover:bg-gray-700 hover:text-white focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white">
            <span class="absolute -inset-0.5" />
            <span class="sr-only">Open main menu</span>
            <Bars3Icon v-if="!open" class="block h-6 w-6" aria-hidden="true" />
            <XMarkIcon v-else class="block h-6 w-6" aria-hidden="true" />
          </DisclosureButton>
        </div>
        <div class="flex flex-1 items-center justify-left sm:items-stretch sm:justify-start">
          <nav class="py-4">
            <div class="container mx-auto flex justify-between items-center">
              <div class="flex flex-shrink-0 items-center">
                <img class="h-8 w-auto" src="/images/mpu-logo-121x121.png" alt="Your Company" />
              </div>
              <div>
                <a class="navbar-caption text-black display-7">
                  語言及翻譯學院 <br>
                  Faculdade de Línguas e Tradução
                </a>
              </div>
              <div class="float-right">
                <div class="flex space-x-4 text-gray-700 relative float-right">
                  <template v-for="item in navigations">
                    <div v-if="item.children" class="relative">
                      <button @click="showSubmenu.value = !showSubmenu.value" class="hover:border-b-2 border-blue-500 flex items-center space-x-1">
                        <span>{{ item.name }}</span>
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                          <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" />
                        </svg>
                      </button>
                      <div v-if="showSubmenu" class="absolute z-10 bg-white rounded-md py-2 mt-2 w-48">
                        <template v-for="subitem in item.children">
                          <NuxtLink to="/service1" class="block px-4 py-2 hover:bg-gray-200 text-gray-700 cursor-pointer">{{ subitem.name }}</NuxtLink>
                        </template>
                      </div>
                    </div>
                    <NuxtLink v-else to="/" class="hover:border-b-2 border-blue-500">{{ item.name }}</NuxtLink>
                  </template>
                </div>
              </div>
            </div>
          </nav>

        </div>
      </div>
    </div>

    <DisclosurePanel class="sm:hidden">
      <div class="space-y-1 px-2 pb-3 pt-2">
        <DisclosureButton v-for="item in navigation" :key="item.name" as="a" :href="item.href"
          :class="[item.current ? 'bg-gray-900 text-white' : 'text-gray-300 hover:bg-gray-700 hover:text-white', 'block rounded-md px-3 py-2 text-base font-medium']"
          :aria-current="item.current ? 'page' : undefined">{{ item.name }}</DisclosureButton>
      </div>
    </DisclosurePanel>
  </Disclosure>

  <div>
    <slot />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { Disclosure, DisclosureButton, DisclosurePanel, Menu, MenuButton, MenuItem, MenuItems } from '@headlessui/vue'
import { Bars3Icon, BellIcon, XMarkIcon } from '@heroicons/vue/24/outline'

const showSubmenu = ref(false);
const mobileMenu = ref(false);

const clickMobileMenu = () => {
  console.log(mobileMenu.value);
  mobileMenu.value = !mobileMenu.value;
};

const navigations = [
  { name: '出版主頁 Início das Publicações', href: '/', current: true },
  {
    name: '出版物 Publicações',
    href: '/publication',
    children: [
      { name: '所有出版物 Todas as Publicações', href: '/products/1' },
      { name: '教材 Materiais Didácticos', href: '/products/2' },
      { name: '著作與參考書籍 Ensaios e Obras de Referência', href: '/products/3' },
    ],
  },
];
</script>