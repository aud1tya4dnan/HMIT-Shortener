<script setup>
import { RouterLink, RouterView } from 'vue-router';
import Navbar from './components/Navigation.vue';
</script>

<template>
  <nav v-if="$route.meta.nav">
    <Navbar />
  </nav>
  <div class="routerview">
    <RouterView />
  </div>
  <footer class="bg-gray-50 dark:bg-gray-900">
    <div class="mx-auto max-w-screen-xl px-4 py-8 sm:px-6 lg:px-8">
      <div class="sm:flex sm:items-center sm:justify-between">
        <div class="flex justify-center text-white sm:justify-start dark:text-white">
          <img src="../src/assets/Icon_KWU.webp" style="width: 40px; height: 40px;"/>
          <span class="ml-2 mt-1 text-xl font-bold">HMIT Store</span>
          
        </div>

        <p class="mt-4 text-center text-sm text-gray-500 lg:mt-0 lg:text-right dark:text-gray-400">
          Copyright &copy; 2024. Made With Patient.
        </p>
      </div>
    </div>
  </footer>
</template>
