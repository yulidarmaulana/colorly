<script setup lang="ts">
import { ref } from 'vue';
import { colors, colorkey } from '../lib/colors'; // Pastikan jalur ini benar

const message = ref<string>('');
const messageColor = ref<string>('');

const copyToClipboard = (color: string) => {
  navigator.clipboard.writeText(color).then(() => {
    message.value = `Kode warna ${color} telah disalin!`;
    messageColor.value = color; // Set warna pesan sesuai dengan warna yang disalin
    setTimeout(() => {
      message.value = '';
    }, 2000);
  }).catch(err => {
    console.error('Gagal menyalin: ', err);
  });
};
</script>

<template>
  <main class="flex flex-col my-6 items-center justify-center max-w-4xl mx-auto pb-8">
    <div class="flex flex-col justify-center items-center">
      <h1 class="font-bold font-family-mono text-4xl mb-4 text-center leading-tight bg-gradient-to-br from-slate-800 to-slate-400 text-transparent bg-clip-text">Colour Palette by Tailwind</h1>
       
      <!-- <div class="flex flex-col items-center justify-center min-h-screen bg-gray-100"> -->
    
    <section class="flex gap-4 bg-white/70 text-center rounded-lg py-2 sticky border border-gray-100/70 backdrop-blur-lg ">
      <template v-for="(shade, index) in colorkey" :key="index">
        <span class="w-14 block font-medium text-sm">{{ shade }}</span>
      </template>
    </section>

    <div v-for="(colorGroup, groupName) in colors" :key="groupName" class="flex items-start my-4">
      <h2 class="text-lg font-bold mr-4 my-auto">{{ groupName }}</h2>
      <div class="flex flex-wrap border w-full gap-2 border-gray-100/10 backdrop-blur-lg">
        <div
          v-for="(color, shade) in colorGroup"
          :key="shade"
          :class="`w-16 h-16 rounded-lg cursor-pointer flex items-center justify-center`"
          :style="{ backgroundColor: color }"
          @click="copyToClipboard(color)"
        >
          <span class="text-dark text-sm">{{ color }}</span>
        </div>
      </div>
    </div>
    
    <section v-if="message" class="border border-gray-100 bg-gray-100 backdrop-blur-lg p-2 rounded-lg mt-4">
      <p :style="{ color: messageColor }" class="text-sm">{{ message }}</p>
    </section>
    </div>
  </main>
</template>

<style>

</style>