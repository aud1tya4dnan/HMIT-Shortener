<!-- <template>
  <div class="navbar bg-primary text-primary-content">
    <div class="navbar-start">
      <div class="dropdown">
        <div tabindex="0" role="button" class="btn btn-ghost btn-circle">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h7" />
          </svg>
        </div>
        <ul tabindex="0" class="menu menu-sm dropdown-content mt-3 z-[1] p-2 shadow rounded-box w-52 bg-primary">
          <li><a href="/">Shorten</a></li>
          <li><a href="/links">Links</a></li>
          <li><a href="/about">About</a></li>
        </ul>
      </div>
    </div>
    <div class="navbar-center">
      <a href="/" class="btn btn-ghost text-xl font-bold"><img src="../assets/Icon_KWU.webp" style="width: 40px; height: 40px;"/> HMIT Store</a>
    </div>

    <div class="navbar-end">
      <div v-if="showdropdown" class="dropdown">
        <div tabindex="0" role="button" class="btn m-1">Username</div>
        <ul tabindex="0" class="dropdown-content z-[1] menu p-2 shadow bg-primary rounded-box w-52">
          <li><a>Item 1</a></li>
          <li><a v-if="isLoggedIn" @click="logout" class="btn btn-bold btn-error font-bold">Logout</a></li>
        </ul>
      </div>

      <a v-else href="/login" class="btn btn-bold btn-primary font-bold">Login</a>
    </div>
  </div>
</template> -->

<template>
  <header class="bg-white dark:bg-gray-900">
    <div class="mx-auto flex h-16 max-w-screen-xl items-center gap-8 px-4 sm:px-6 lg:px-8">
      <a class="block text-teal-600 dark:text-teal-300" href="#">
        <img src="../assets/Icon_KWU.webp" style="width: 40px; height: 40px;" />
      </a>

      <div class="flex flex-1 items-center justify-end md:justify-between">
        <nav aria-label="Global" class="hidden md:block">
          <ul class="flex items-center gap-6 text-sm">
            <li>
              <a class="text-gray-500 transition hover:text-gray-500/75 dark:text-white dark:hover:text-white/75"
                href="/">
                Dashboard
              </a>
            </li>

            <li>
              <a class="text-gray-500 transition hover:text-gray-500/75 dark:text-white dark:hover:text-white/75"
                href="/links">
                Links
              </a>
            </li>

            <li>
              <a class="text-gray-500 transition hover:text-gray-500/75 dark:text-white dark:hover:text-white/75"
                href="#">
                About
              </a>
            </li>
          </ul>
        </nav>

        <div class="flex items-center gap-4">
          <div class="sm:flex sm:gap-4">
            <a v-if="showLoginButton"
              class="block rounded-md bg-teal-600 px-5 py-2.5 text-sm font-medium text-white transition hover:bg-teal-700 dark:hover:bg-teal-500"
              href="/login">
              Login
            </a>
            <a v-if="isLoggedIn"
              class="block rounded-md bg-gray-100 px-5 py-2.5 text-sm font-medium text-white transition hover:text-white dark:bg-red-800 dark:hover:bg-red-700"
              @click="logout()">
              Logout
            </a>
          </div>

          <!-- <button
            @click="showdropdown = !showdropdown"
            class="block rounded bg-gray-100 p-2.5 text-gray-600 transition hover:text-gray-600/75 md:hidden dark:bg-gray-800 dark:text-white dark:hover:text-white/75">
            <span class="sr-only">Toggle menu</span>
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24"
              stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
          </button> -->

          <aside>
            
          </aside>

        </div>
      </div>
    </div>
  </header>
</template>

<script>
// import api from "../api/url.js";
// import axios from 'axios';

export default {
  data() {
    return {
      // Contoh sederhana, Anda perlu mengganti ini dengan logika sesungguhnya
      isLoggedIn: false,
      showLoginButton: true,
      showdropdown: false,
    };
  },
  methods: {
    logout() {
      // Logika untuk logout
      this.isLoggedIn = false;
      this.showLoginButton = true;
      localStorage.clear();
      sessionStorage.clear();
    },

    async checkLoginStatus() {
      let uid = localStorage.getItem("uid");
      if (uid !== null || uid !== "" || uid !== "auth/netowork-error") {
        return true;
      }
      return false; // atau false, tergantung status pengguna
    },

    async checkTime() {
      let expired = localStorage.getItem("expired");
      
      if (expired < Date.now()) {
        this.logout();
      }
    }

  },
  mounted() {
    this.isLoggedIn = this.checkLoginStatus();
    if (this.isLoggedIn === true) {
      this.showLoginButton = false;
      setInterval(this.checkTime, 1000);
    } else {
      this.logout();
    }
  },
};
</script>
