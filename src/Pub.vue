<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';
import Publication from './components/Publication.vue';
import Foot from './components/Foot.vue';

/** publications **/
import { publications } from '@/js/publications.js';
</script>

<template>
<div class="bg-white dark:bg-neutral-900 text-black dark:text-white">

  <header class="flex flex-wrap z-50 w-full py-6 lg:justify-start lg:flex-nowrap translate-y-0 transition-all duration-300">
    <nav class="max-w-7xl w-full flex flex-wrap lg:grid lg:grid-cols-12 basis-full items-center px-4 md:px-6 lg:px-8 mx-auto">
      <div class="flex items-center gap-x-1 lg:gap-x-2 lg:col-span-3 lg:col-start-1">
        <a class="flex-none rounded-xl text-2xl inline-block font-semibold" href="/" aria-label="Preline">
          <img class="inline-block size-12.5 rounded-lg" src="@/assets/img/logo.jpg" alt="Logo" />
          <span class="inline-block ms-3 mt-3">PIE Lab</span>
        </a>
      </div>

      <div class="flex items-center gap-x-1 lg:gap-x-2 lg:col-span-6 lg:col-start-4 justify-center">
        <span class="text-xl font-semibold ms-6 pt-1">Publications</span>
      </div>

      <div class="flex items-center gap-x-1 lg:gap-x-2 lg:col-span-3 lg:col-end-13 ml-auto py-1">
        <button type="button" class="hs-dark-mode hs-dark-mode-active:hidden flex items-center gap-x-2 py-2 px-3 bg-white border border-gray-200 rounded-full text-sm text-black hover:bg-neutral-100" data-hs-theme-click-value="dark">
          <svg class="shrink-0 size-4" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M12 3a6 6 0 0 0 9 9 9 9 0 1 1-9-9Z"></path>
          </svg>
          Dark
        </button>
        <button type="button" class="hs-dark-mode hs-dark-mode-active:inline-flex hidden items-center gap-x-2 py-2 px-3 bg-white/10 rounded-full text-sm text-white hover:bg-white/20" data-hs-theme-click-value="light">
          <svg class="shrink-0 size-4" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <circle cx="12" cy="12" r="4"></circle>
            <path d="M12 2v2"></path>
            <path d="M12 20v2"></path>
            <path d="m4.93 4.93 1.41 1.41"></path>
            <path d="m17.66 17.66 1.41 1.41"></path>
            <path d="M2 12h2"></path>
            <path d="M20 12h2"></path>
            <path d="m6.34 17.66-1.41 1.41"></path>
            <path d="m19.07 4.93-1.41 1.41"></path>
          </svg>
          Light
        </button>
      </div>
    </nav>
  </header>

  <section id="publications">
    <div class="max-w-7xl px-4 sm:px-6 lg:px-8 py-12 lg:py-16 mx-auto">
      <div class="flex flex-col justify-center items-center">
        <Publication v-for="(pub, index) in publications" :key="index"
          :title="pub.title"
          :authors="pub.authors"
          :publisher="pub.publisher"
          :links="pub.links">
        </Publication>
      </div>
    </div>
  </section>

  <Foot></Foot>
</div>
</template>