<template>

<header class="bg-white shadow">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex justify-between h-16">
      <div class="flex">
        <div class="flex-shrink-0 flex items-center">
          <img src="/images/mpu-logo-121x121.png" alt="MPU" width="50">
          <a class="font-bold text-lg" href="/">語言及翻譯學院&nbsp;<br>Faculdade de Línguas e Tradução</a>
        </div>
      </div>
      <div class="-mr-2 flex items-center sm:hidden">
        <button type="button" @click="mobileMenu=!mobileMenu" class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-gray-500 hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500" aria-controls="mobile-menu" aria-expanded="false">
          <span class="sr-only">Open main menu</span>
          <svg class="h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" aria-hidden="true">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          </svg>
        </button>
      </div>

      <div class="hidden sm:ml-6 sm:flex sm:space-x-8 pt-5">
        <template v-for="item in menus">
          <div v-if="item.children" class="relative">
            <button @click="showSubmenu=!showSubmenu" class="hover:border-b-2 border-blue-500 flex items-center space-x-1">
              <span>{{ item.name }}</span>
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" />
              </svg>
            </button>
            <div v-if="showSubmenu" class="absolute z-10 bg-white rounded-md py-2 mt-2 w-48">
              <template v-for="subItem in item.children">
                <a :href="subItem.href" class="block px-4 py-2 hover:bg-gray-200 text-gray-700 cursor-pointer">{{ subItem.name }}</a>
              </template>
            </div>
          </div>
          <a v-else href="/" class="hover:border-b-2 border-blue-500 mb-5">{{ item.name }}</a>
        </template>
      </div>
    </div>
  </div>

  <!-- Mobile menu -->
  <div class="sm:hidden" v-if="mobileMenu">
    <div class="pt-2 pb-4 space-y-1">
      <template v-for="item in menus">
        <NuxtLink href="#" class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-gray-900 hover:bg-gray-50">{{ item.name }}</NuxtLink>
        <div v-if="item.children" class="pl-5">
          <NuxtLink v-for="subItem in item.children" :href="subItem.href" class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-gray-900 hover:bg-gray-50">{{ subItem.name }}</NuxtLink>
        </div>
      </template>
    </div>
  </div>
</header>


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

const menus = [
  { name: '出版主頁 Início das Publicações', href: '/', current: true },
  {
    name: '出版物 Publicações',
    href: '/publication',
    children: [
      { name: '所有出版物 Todas as Publicações', href: '/publications?cat=all' },
      { name: '教材 Materiais Didácticos', href: '/publications?cat=material' },
      { name: '著作與參考書籍 Ensaios e Obras de Referência', href: '/publications?cat=book' },
    ],
  },
];
</script>