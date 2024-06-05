<template>
  <div class="background-container ">
    <div class="container">
      <h1 class="text-4xl font-sans text-black font-bold">HMIT Shortener Link</h1>
      <div class="label">
        <label class="text-4xl font-sans text-black font-light">Short Your Url! 🚀 </label>
        <input
          type="text"
          id="userinput"
          class="input input-bordered w-96 bg-white max-w-xs border-2 border-blue-300 rounded px-4 py-2 mt-8"
          placeholder="Enter your url"
          v-model="longurl"
        />
        <input
          type="text"
          id="shorturl"
          class="input input-bordered w-full bg-white max-w-xs border-2 border-blue-300 rounded px-4 py-2 mt-4"
          placeholder="Enter your shorten link"
          v-model="shorturl"
        />
        <button
          class="bg-blue-500 hover:bg-blue-300 text-white font-bold py-2 px-4 rounded mt-4"
          @click="postLink()"
          @keyup.enter="postLink()"
        >
          Shorten
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import api from "../api/url.js";
import axios from 'axios';

export default {
  data() {
    return {
      longurl: "",
      shorturl: "",
    };
  },
  methods: {
    async postLink() {
        let uid = localStorage.getItem('uid');
      console.log(this.longurl);
      const send = await axios
        .post(api + "login", {
          flink: this.longurl,
          slink: this.shorturl,
          uid: uid,
          uses: 0,
        })
        .then((response) => {
          // console.log(response);
          this.$router.push("/links");
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style scoped>
.background-container {
  display: flex; /* Menetapkan display ke flex */
  flex-direction: column; /* Mengubah arah flex items menjadi vertikal */
  justify-content: center; /* Menengahkan konten secara horizontal */
  align-items: center; /* Menengahkan konten secara vertikal */
  height: 800px; /* Mengatur tinggi container agar mengisi layar penuh */
  background-image: url('../assets/BG-upscaled.webp');
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
}

.label {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
