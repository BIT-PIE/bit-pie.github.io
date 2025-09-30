<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';

/** footer **/
const currentYear = new Date().getFullYear();
</script>

<template>
  <footer class="w-full max-w-7xl py-6 md:pt-0 px-4 sm:px-6 lg:px-8 mx-auto">
    <hr class="border-0.5 border-neutral-200 dark:border-neutral-800">
    <div class="grid grid-cols-1 items-center gap-5 py-6">
      <div class="text-center text-neutral-700 dark:text-neutral-300">
        <div class="pb-3">© {{ currentYear }} PIE Lab @ BIT.</div>
        <div class="pb-3 text-sm">The site is deployed on <a class="simple-link" href="https://pages.github.com/">Github Pages</a>. The source is licensed under <a class="simple-link" href="https://creativecommons.org/licenses/by-nc-nd/4.0/"> CC-BY-NC_ND</a>.</div>
      </div>
    </div>
  </footer>
</template>