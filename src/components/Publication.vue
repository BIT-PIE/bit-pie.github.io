<script setup>
import { computed } from 'vue';

const { title, authors, publisher, links } = defineProps({
  title: {
    type: String,
    default: ''
  },
  authors: {
    type: String,
    default: ''
  },
  publisher: {
    type: String,
    default: ''
  },
  links: {
    type: Object,
    default: () => ({})
  }
});

const validLinks = computed(() => {
  let valid = {};
  for (const [key, value] of Object.entries(links)) {
    if (key !== 'image' && value && value.trim() !== '' && value !== '#' && value !== '/') {
      valid[key] = value;
    }
  }
  return valid;
});
</script>

<template>
<div class="w-4/5 flex border border-gray-200 border-t-4 border-t-blue-500 shadow-2xs rounded-xl mx-3 lg:mx-6 my-3 dark:border-neutral-700 dark:border-t-blue-500 dark:shadow-neutral-700">
  <div class="flex-shrink-0 px-4 py-4">
    <img v-if="links.image" :src="links.image" class="w-32 h-auto md:w-56 lg:w-64 object-cover rounded-t-lg md:rounded-t-none md:rounded-s-lg">
  </div>
  
  <div class="p-4 md:p-5">
    <h3 class="text-lg font-bold text-gray-800 dark:text-white">
      <a :href="links.web ? links.web : links.paper" class="hover:underline">{{ title }}</a>
    </h3>
    <p class="mt-1 text-sm text-gray-600 dark:text-neutral-400">
      <span v-html="publisher"></span>
    </p>
    <p class="mt-2 text-gray-500 dark:text-neutral-400">
      {{ authors }}
    </p>
    <div class="mt-4 flex flex-wrap gap-2">
      <a v-for="(link, key) in validLinks" :key="key" :href="link" target="_blank"
        class="inline-flex items-center gap-x-1.5 py-1.5 px-3 rounded-full text-xs font-medium border border-blue-600 text-blue-600 dark:border-blue-400 dark:text-blue-400">
        {{ key }}
      </a>
    </div>
  </div>
</div>
</template>