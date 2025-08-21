<script setup>
import { computed } from 'vue';
const MEMBERS_EACH_ROW = 5; // number of members in each row
const widthEachMember = computed(() => {
  return `lg:w-1/${MEMBERS_EACH_ROW + 1}`;
});

const {enName, chName, description, links } = defineProps({
  isAlumni: {
    type: Boolean,
    default: false
  },
  enName: {
    type: String,
    default: ''
  },
  chName: {
    type: String,
    default: ''
  },
  description: {
    type: String,
    default: ''
  },
  links: {
    type: Object,
    default: () => ({})
  }
});

const avatarLink = computed(() => {
  if (links && links.avatar) {
    return links.avatar;
  }
  return 'https://placehold.co/300x300';
});
</script>

<template>
<div :class="widthEachMember" class="max-w-72 w-1/1 lg:w-1/6 px-3">
  <div v-if="!isAlumni" class="max-w-36 aspect-1/1 overflow-hidden rounded-full mx-auto">
    <img class="size-full object-cover rounded-full" :src="avatarLink" alt="Person Image">
  </div>

  <h2 v-if="!isAlumni" class="mt-4 font-semibold text-center">{{ enName }}{{ chName ? ` (${chName})` : '' }}</h2>
  <h2 v-else class="mt-4 font-semibold text-center">
    <span v-if="links.website"><a :href="links.website" class="simple-link">{{ enName }}</a></span>
    <span v-else>{{ enName }}</span>
  </h2>
  <h3 class="text-sm text-center text-gray-500 dark:text-neutral-400">{{ description }}</h3>

  <div v-if="!isAlumni" class="mt-2 flex gap-4 justify-center">
    <a v-if="links.email" :href="`mailto:${links.email}`" class="inline-flex justify-center items-center size-6 rounded-full simple-link">
      <svg t="1755680125904" class="icon fill-current" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="7470"><path d="M926.47619 355.644952V780.190476a73.142857 73.142857 0 0 1-73.142857 73.142857H170.666667a73.142857 73.142857 0 0 1-73.142857-73.142857V355.644952l304.103619 257.828572a170.666667 170.666667 0 0 0 220.745142 0L926.47619 355.644952zM853.333333 170.666667a74.044952 74.044952 0 0 1 26.087619 4.778666 72.704 72.704 0 0 1 30.622477 22.186667 73.508571 73.508571 0 0 1 10.678857 17.67619c3.169524 7.509333 5.12 15.652571 5.607619 24.210286L926.47619 243.809524v24.380952L559.469714 581.241905a73.142857 73.142857 0 0 1-91.306666 2.901333l-3.632762-2.925714L97.52381 268.190476v-24.380952a72.899048 72.899048 0 0 1 40.155428-65.292191A72.97219 72.97219 0 0 1 170.666667 170.666667h682.666666z" p-id="7471"></path></svg>
    </a>
    <a v-if="links.github" :href="links.github" target="_blank" class="inline-flex justify-center items-center size-6 rounded-full simple-link">
      <svg t="1755680210070" class="icon fill-current" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="5467"><path d="M511.6 76.3C264.3 76.2 64 276.4 64 523.5 64 718.9 189.3 885 363.8 946c23.5 5.9 19.9-10.8 19.9-22.2v-77.5c-135.7 15.9-141.2-73.9-150.3-88.9C215 726 171.5 718 184.5 703c30.9-15.9 62.4 4 98.9 57.9 26.4 39.1 77.9 32.5 104 26 5.7-23.5 17.9-44.5 34.7-60.8-140.6-25.2-199.2-111-199.2-213 0-49.5 16.3-95 48.3-131.7-20.4-60.5 1.9-112.3 4.9-120 58.1-5.2 118.5 41.6 123.2 45.3 33-8.9 70.7-13.6 112.9-13.6 42.4 0 80.2 4.9 113.5 13.9 11.3-8.6 67.3-48.8 121.3-43.9 2.9 7.7 24.7 58.3 5.5 118 32.4 36.8 48.9 82.7 48.9 132.3 0 102.2-59 188.1-200 212.9 23.5 23.2 38.1 55.4 38.1 91v112.5c0.8 9 0 17.9 15 17.9 177.1-59.7 304.6-227 304.6-424.1 0-247.2-200.4-447.3-447.5-447.3z" p-id="5468"></path></svg>
    </a>
    <a v-if="links.website" :href="links.website" target="_blank" class="inline-flex justify-center items-center size-6 rounded-full simple-link">
      <svg t="1755680280647" class="icon fill-current" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="9431"><path d="M640 790.528H297.504v-0.096l86.496 0.032v-118.88c0-0.8 0.224-1.536 0.224-2.304 1.28-69.6 57.984-125.888 127.776-125.888s126.496 56.32 127.776 125.888c0 0.768 0.224 1.504 0.224 2.304v118.944z m240.896-427.68L800 309.856V207.168a32 32 0 1 0-64 0v60.8l-206.464-135.328A31.296 31.296 0 0 0 511.424 128a31.168 31.168 0 0 0-17.6 4.64L142.464 362.88a32 32 0 0 0 35.072 53.536L192 406.912V800c0 30.08 27.168 54.592 60.576 54.592h518.848C804.832 854.56 832 830.08 832 800V407.36l13.856 9.056a31.968 31.968 0 0 0 35.04-53.536z" p-id="9432"></path></svg>
    </a>
  </div>
</div>
</template>
