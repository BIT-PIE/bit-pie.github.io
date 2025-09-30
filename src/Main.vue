<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';
import Avatar from '@/components/Avatar.vue';
import Publication from './components/Publication.vue';
import Foot from '@/components/Foot.vue';

/** navbar **/
import scrollSpy from '@/js/scrollspy';
const scrolled = ref(false);
const handleScroll = () => {
  scrolled.value = window.scrollY > 12;
}
 
onMounted(() => {
  window.addEventListener("scroll", handleScroll);

  // Initialize scrollspy
  scrollSpy('#hs-header-links', {
    sectionSelector: 'section',
    targetSelector: 'a',
    offset: 64,
    activeClass: 'active-nav-link',
  })
})

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
})

/** home **/
const teaserLink = '/images/teaser-1.comp.jpg'

/** news **/
import { news } from '@/js/news.js';
const sortedNews = computed(() => {
  return news.slice(0, 10).sort((a, b) => new Date(b.date) - new Date(a.date));
});

/** team **/
import { ROLE, members } from '@/js/team.js';
const faculty = computed(() => {
  return members.filter(member => member.role === ROLE.faculty).sort((a, b) => a.enName.split(' ').reverse().join(' ').localeCompare(b.enName.split(' ').reverse().join(' ')));
});
const phd = computed(() => {
  return members.filter(member => member.role === ROLE.student && member.description.toLowerCase().includes('phd')).sort((a, b) => a.enName.split(' ').reverse().join(' ').localeCompare(b.enName.split(' ').reverse().join(' ')));
});
const master = computed(() => {
  return members.filter(member => member.role === ROLE.student && member.description.toLowerCase().includes('master')).sort((a, b) => a.enName.split(' ').reverse().join(' ').localeCompare(b.enName.split(' ').reverse().join(' ')));
});
const undergraduate = computed(() => {
  return members.filter(member => member.role === ROLE.undergraduate).sort((a, b) => a.enName.split(' ').reverse().join(' ').localeCompare(b.enName.split(' ').reverse().join(' ')));
});
const alumni = computed(() => {
  let phd = members.filter(member => member.role === ROLE.alumni && member.description.toLowerCase().includes('phd')).sort((a, b) => a.enName.split(' ').reverse().join(' ').localeCompare(b.enName.split(' ').reverse().join(' ')));
  let master = members.filter(member => member.role === ROLE.alumni && member.description.toLowerCase().includes('master')).sort((a, b) => a.enName.split(' ').reverse().join(' ').localeCompare(b.enName.split(' ').reverse().join(' ')));
  return [...phd, ...master]
});

/** publications **/
import { publications } from '@/js/publications.js';
const selectedPublications = computed(() => {
  let selectedPublications = publications.slice(0, 5);
  // Remove images for selected publications to speed up loading
  selectedPublications.forEach(pub => {
    if (pub.links && pub.links.image) {
      pub.links.image = '';
    }
  });
  return selectedPublications;
});

/** photos **/
import { photos } from '@/js/photos.js';
const photosGroup1 = computed(() => {
  return photos.slice(0, Math.ceil(photos.length / 2));
})
const photosGroup2 = computed(() => {
  return photos.slice(Math.ceil(photos.length / 2));
})
</script>

<template>
<div :class="{ 'scrolled': scrolled }" class="bg-white dark:bg-neutral-900 text-black dark:text-white">

  <header class="fixed top-0 left-0 flex flex-wrap z-50 w-full py-6 lg:justify-start lg:flex-nowrap translate-y-0 transition-all duration-300">
    <nav class="relative max-w-7xl w-full flex flex-wrap lg:grid lg:grid-cols-12 basis-full items-center px-4 md:px-6 lg:px-8 mx-auto">
      <div class="lg:col-span-3 flex items-center header-left transition-all duration-100">
        <a class="flex-none rounded-xl text-2xl inline-block font-semibold" href="/" aria-label="Preline">
          <img class="inline-block size-12.5 rounded-lg" src="@/assets/img/logo.jpg" alt="Logo" />
          <span class="inline-block ms-3 mt-3">PIE Lab</span>
        </a>
      </div>

      <div class="flex items-center gap-x-1 lg:gap-x-2 ms-auto py-1 lg:ps-6 lg:order-3 lg:col-span-3 header-right transition-all duration-100">
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

        <div class="lg:hidden">
          <button type="button"
            id="hs-header-collapse-button" data-hs-collapse="#hs-header-collapse"
            class="hs-collapse-toggle size-9.5 flex justify-center items-center text-sm font-semibold rounded-xl border border-gray-200 text-black hover:bg-neutral-100 dark:text-white dark:border-neutral-700 dark:hover:bg-neutral-700">
            <svg class="hs-collapse-open:hidden shrink-0 size-4" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <line x1="3" x2="21" y1="6" y2="6" />
              <line x1="3" x2="21" y1="12" y2="12" />
              <line x1="3" x2="21" y1="18" y2="18" />
            </svg>
            <svg class="hs-collapse-open:block hidden shrink-0 size-4" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M18 6 6 18" />
              <path d="m6 6 12 12" />
            </svg>
          </button>
        </div>
      </div>

      <div id="hs-header-collapse" class="hs-collapse hidden overflow-hidden basis-full py-3 grow lg:block lg:w-auto lg:basis-auto lg:order-2 lg:col-span-6 header-center transition-all duration-300">
        <div id="hs-header-links" class="flex flex-col gap-y-4 gap-x-0 mt-5 lg:flex-row lg:justify-center lg:items-center lg:gap-y-0 lg:gap-x-7 lg:mt-0">
          <a class="inline-block text-black hover:text-gray-500 dark:hover:text-neutral-300; dark:text-white active-nav-link" href="#home">Home</a>
          <a class="inline-block text-black hover:text-gray-500 dark:hover:text-neutral-300; dark:text-white" href="#news">News</a>
          <a class="inline-block text-black hover:text-gray-500 dark:hover:text-neutral-300; dark:text-white" href="#publications">Publications</a>
          <a class="inline-block text-black hover:text-gray-500 dark:hover:text-neutral-300; dark:text-white" href="#team">Team</a>
          <a class="inline-block text-black hover:text-gray-500 dark:hover:text-neutral-300; dark:text-white" href="#photos">Photos</a>
        </div>
      </div>
    </nav>
  </header>

  <section id="home">
    <div class="h-32"></div> <!-- Spacer for fixed header -->

    <div class="max-w-7xl px-4 sm:px-6 lg:px-8 mx-auto">
      <div :style="{ backgroundImage: `url(${teaserLink})` }"
        class="h-120 md:h-[80dvh] 2xl:h-auto 2xl:aspect-[2/1] w-full flex flex-col bg-cover bg-center bg-no-repeat rounded-2xl">
        <div class="mt-auto w-2/3 md:max-w-lg ps-5 pb-5 md:ps-10 md:pb-10">
          <h1 class="text-xl md:text-3xl lg:text-5xl text-white text-yellow-400">
           PIE Lab @ BIT
          </h1>
        </div>
      </div>
    </div>

    <div class="max-w-7xl px-6 lg:px-12 py-3 lg:py-6 mx-auto">
      <blockquote class="relative ms-6 p-6 mt-12 mb-6 rounded-xl">
        <svg class="absolute -top-6 -start-8 size-16 text-gray-100 dark:text-neutral-700" width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
          <path d="M7.39762 10.3C7.39762 11.0733 7.14888 11.7 6.6514 12.18C6.15392 12.6333 5.52552 12.86 4.76621 12.86C3.84979 12.86 3.09047 12.5533 2.48825 11.94C1.91222 11.3266 1.62421 10.4467 1.62421 9.29999C1.62421 8.07332 1.96459 6.87332 2.64535 5.69999C3.35231 4.49999 4.33418 3.55332 5.59098 2.85999L6.4943 4.25999C5.81354 4.73999 5.26369 5.27332 4.84476 5.85999C4.45201 6.44666 4.19017 7.12666 4.05926 7.89999C4.29491 7.79332 4.56983 7.73999 4.88403 7.73999C5.61716 7.73999 6.21938 7.97999 6.69067 8.45999C7.16197 8.93999 7.39762 9.55333 7.39762 10.3ZM14.6242 10.3C14.6242 11.0733 14.3755 11.7 13.878 12.18C13.3805 12.6333 12.7521 12.86 11.9928 12.86C11.0764 12.86 10.3171 12.5533 9.71484 11.94C9.13881 11.3266 8.85079 10.4467 8.85079 9.29999C8.85079 8.07332 9.19117 6.87332 9.87194 5.69999C10.5789 4.49999 11.5608 3.55332 12.8176 2.85999L13.7209 4.25999C13.0401 4.73999 12.4903 5.27332 12.0713 5.85999C11.6786 6.44666 11.4168 7.12666 11.2858 7.89999C11.5215 7.79332 11.7964 7.73999 12.1106 7.73999C12.8437 7.73999 13.446 7.97999 13.9173 8.45999C14.3886 8.93999 14.6242 9.55333 14.6242 10.3Z" fill="currentColor"></path>
        </svg>
        <div class="relative z-10">
          <p class="text-lg text-justify"><em>
            The <span class="font-semibold">Perception, Interaction, and Embodiment Lab (PIE Lab)</span>, affiliated with the <a class="simple-link" href="https://cs.bit.edu.cn/">School of Computer Science & Technology</a> at <a class="simple-link" href="https://bit.edu.cn/">Beijing Institute of Technology (BIT)</a>, aiming to build intelligent systems that see, interact, and act in the world.
          </em></p>
        </div>
      </blockquote>

      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
        <div class="flex flex-col bg-white border border-gray-200 shadow-2xs rounded-xl p-4 md:p-5 dark:bg-neutral-900 dark:border-neutral-700 dark:shadow-neutral-700/70">
          <h3 class="text-lg font-bold text-gray-800 dark:text-white">
            Perception
          </h3>
          <!-- <p class="mt-1 text-xs font-medium uppercase text-gray-500 dark:text-neutral-500">
            Card subtitle
          </p> -->
          <p class="mt-2 text-gray-500 dark:text-neutral-400 text-justify">
            We focus on multi-sensor perception and fusion, integrating vision, LiDAR, IMU, and other modalities to support applications in unmanned platforms.
          </p>
        </div>

        <div class="flex flex-col bg-white border border-gray-200 shadow-2xs rounded-xl p-4 md:p-5 dark:bg-neutral-900 dark:border-neutral-700 dark:shadow-neutral-700/70">
          <h3 class="text-lg font-bold text-gray-800 dark:text-white">
            Interaction
          </h3>
          <!-- <p class="mt-1 text-xs font-medium uppercase text-gray-500 dark:text-neutral-500">
            Card subtitle
          </p> -->
          <p class="mt-2 text-gray-500 dark:text-neutral-400 text-justify">
            We explore human-computer interaction, with an emphasis on intelligent content generation for VR/AR applications to enhance immersive experiences.
          </p>
        </div>

        <div class="flex flex-col bg-white border border-gray-200 shadow-2xs rounded-xl p-4 md:p-5 dark:bg-neutral-900 dark:border-neutral-700 dark:shadow-neutral-700/70">
          <h3 class="text-lg font-bold text-gray-800 dark:text-white">
            Embodiment
          </h3>
          <!-- <p class="mt-1 text-xs font-medium uppercase text-gray-500 dark:text-neutral-500">
            Card subtitle
          </p> -->
          <p class="mt-2 text-gray-500 dark:text-neutral-400 text-justify">
            We aim to endow embodied AI agents with fundamental motor skills, empowering navigation and locomotion for both wheeled and legged robots.
          </p>
        </div>
      </div>
    </div>
  </section>

  <section id="news">
    <div class="max-w-7xl px-4 lg:px-8 py-12 lg:py-16 mx-auto">
      <div class="mb-6 sm:mb-10 max-w-2xl text-center mx-auto">
        <h1 class="font-medium text-black text-3xl sm:text-4xl dark:text-white">
          Recent News
        </h1>
      </div>
      
      <div class="px-6 md:px-12">
        <ul class="list-disc list-inside">
          <li v-for="(item, index) in sortedNews" :key="index" class="mb-2">
            <span class="text-lg font-semibold">[{{ item.date }}]</span>
            <span class="text-lg ms-2" v-html="item.content"></span>
          </li>
        </ul>
      </div>
    </div>
  </section>

  <section id="publications">
    <div class="max-w-7xl px-4 sm:px-6 lg:px-8 py-12 lg:py-16 mx-auto">
      <div class="mb-6 sm:mb-10 max-w-2xl text-center mx-auto">
        <h1 class="font-medium text-black text-3xl sm:text-4xl dark:text-white">
          Selected Publications
        </h1>
      </div>

      <div class="flex flex-col justify-center items-center">
        <Publication v-for="(pub, index) in selectedPublications" :key="index"
          :title="pub.title"
          :authors="pub.authors"
          :publisher="pub.publisher"
          :links="pub.links">
        </Publication>
      </div>

      <div class="mt-6 text-center">
        <a class="inline-flex items-center gap-x-1 text-sm decoration-2 font-semibold simple-link" href="/publication">
          Full publication list
          <svg class="shrink-0 size-4" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m9 18 6-6-6-6"/></svg>
        </a>
      </div>
    </div>
  </section>

  <section id="team">
    <div class="max-w-7xl px-4 sm:px-6 lg:px-8 py-12 lg:py-16 mx-auto">
      <div class="mb-6 sm:mb-10 max-w-2xl text-center mx-auto">
        <h1 class="font-medium text-black text-3xl sm:text-4xl dark:text-white">
          Team Members
        </h1>
      </div>

      <div class="text-center text-2xl font-semibold pt-3 pb-6">
        Faculty
      </div>
      <div class="flex flex-wrap justify-center gap-6">
        <Avatar v-for="(member, index) in faculty" :key="index"
          :enName="member.enName"
          :chName="member.chName"
          :description="member.description"
          :links="member.links">
        </Avatar>
      </div>

      <div v-if="phd.length > 0" class="text-center text-2xl font-semibold pt-12 pb-6">
        PhD Student
      </div>
      <div v-if="phd.length > 0" class="flex flex-wrap justify-center gap-6">
        <Avatar v-for="(member, index) in phd" :key="index"
          :enName="member.enName"
          :chName="member.chName"
          :description="member.description"
          :links="member.links">
        </Avatar>
      </div>

      <div v-if="master.length > 0" class="text-center text-2xl font-semibold pt-12 pb-6">
        Master Student
      </div>
      <div v-if="master.length > 0" class="flex flex-wrap justify-center gap-6">
        <Avatar v-for="(member, index) in master" :key="index"
          :enName="member.enName"
          :chName="member.chName"
          :description="member.description"
          :links="member.links">
        </Avatar>
      </div>

      <div v-if="undergraduate.length > 0" class="text-center text-2xl font-semibold pt-12 pb-6">
        Undergrad Student
      </div>
      <div v-if="undergraduate.length > 0" class="flex flex-wrap justify-center gap-6">
        <Avatar v-for="(member, index) in undergraduate" :key="index"
          :enName="member.enName"
          :chName="member.chName"
          :description="member.description"
          :links="member.links">
        </Avatar>
      </div>

      <div v-if="alumni.length > 0" class="text-center text-2xl font-semibold pt-12 pb-3">
        Alumni
      </div>
      <div v-if="alumni.length > 0" class="flex flex-wrap justify-center gap-6 pb-6">
        <Avatar v-for="(member, index) in alumni.slice(0, 5)" :key="index"
          :isAlumni="true"
          :enName="member.enName"
          :chName="member.chName"
          :description="member.description"
          :links="member.links">
        </Avatar>
      </div>
      <div v-if="alumni.length > 5" id="hs-show-hide-collapse-heading" class="hs-collapse hidden w-full overflow-hidden transition-[height] duration-300 flex flex-wrap justify-center gap-6">
        <Avatar v-for="(member, index) in alumni.slice(5)" :key="index"
          :isAlumni="true"
          :enName="member.enName"
          :chName="member.chName"
          :description="member.description"
          :links="member.links">
        </Avatar>
      </div>
      <p v-if="alumni.length > 5" class="mt-6 text-center">
        <button type="button" class="hs-collapse-toggle inline-flex items-center gap-x-1 text-sm decoration-2 font-semibold simple-link" id="hs-show-hide-collapse" data-hs-collapse="#hs-show-hide-collapse-heading">
          <span class="hs-collapse-open:hidden">Show more</span>
          <span class="hs-collapse-open:block hidden">Show less</span>
          <svg class="hs-collapse-open:rotate-180 shrink-0 size-4" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="m6 9 6 6 6-6"></path>
          </svg>
        </button>
      </p>
    </div>
  </section>

  <section id="photos">
    <div class="w-[100vdw] py-12 lg:py-16 mx-auto">
      <div class="mb-6 sm:mb-10 max-w-2xl text-center mx-auto">
        <h1 class="font-medium text-black text-3xl sm:text-4xl dark:text-white">
          Lab Photos
        </h1>
      </div>

      <div class="overflow-hidden w-full py-5">
        <div class="flex gap-6 animate-slide">
          <img v-for="(photo, index) in photosGroup1" :key="index" :src="photo" class="rounded-xl h-48 xl:h-64 3xl:h-80 w-auto" />
          <img v-for="(photo, index) in photosGroup1" :key="index + 2 * photosGroup1.length" :src="photo" class="rounded-xl h-48 xl:h-64 3xl:h-80 w-auto" /> <!-- Duplicate to create a continuous scroll effect -->
        </div>
      </div>

      <div class="overflow-hidden w-full py-5">
        <div class="flex gap-6 animate-slide">
          <img v-for="(photo, index) in photosGroup2" :key="index" :src="photo" class="rounded-xl h-48 xl:h-64 3xl:h-80 w-auto" />
          <img v-for="(photo, index) in photosGroup2" :key="index + 2 * photosGroup2.length" :src="photo" class="rounded-xl h-48 xl:h-64 3xl:h-80 w-auto" /> <!-- Duplicate to create a continuous scroll effect -->
        </div>
      </div>
    </div>
  </section>

  <Foot></Foot>
</div>
</template>
