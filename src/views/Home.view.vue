<script setup>
import { ref, computed } from 'vue';
import scrollTo from '@/utils/scrollTo.js';
import projects from '@/assets/projects.json';

const featuredProjects = computed(() => {
  return [...projects]
    .filter(project => project.featured)
    .sort((a, b) => b.id - a.id)
    .slice(0, 3);
});

const latestProjects = computed(() => {
  return [...projects]
    .sort((a, b) => b.id - a.id)
    .slice(0, 3);
});

</script>

<template>
  <main class="w-full min-h-screen text-gray-900 font-mono bg-gradient-to-r from-blue-100 via-purple-100 to-pink-100">
    <section class="h-screen flex flex-col items-center justify-center text-center px-6 relative bg-gradient-to-b from-black/5 via-transparent to-transparent">
      <h1 class="text-6xl md:text-8xl font-semibold drop-shadow-lg mb-4 select-none animate-fade-in bg-gradient-to-r from-blue-500 via-purple-400 to-pink-400 bg-clip-text text-transparent">LookAtFr3sn0</h1>
      <div class="flex gap-4 text-sm md:text-lg lg:text-xl text-gray-600 mb-8 items-center justify-center">
        <p>Software developer</p>
        <span class="h-4 w-px rounded-full bg-gray-400 inline-block"></span>
        <p>Game developer</p>
        <span class="h-4 w-px rounded-full bg-gray-400 inline-block"></span>
        <p>3D artist</p>
      </div>
      <button
        class="cursor-pointer border border-gray-900 px-6 py-2 text-sm uppercase tracking-widest rounded-full bg-white/40 backdrop-blur-md shadow-md hover:bg-gray-900 hover:text-white transition-all duration-200 font-semibold select-none"
        @click="scrollTo('featured')"
      >
        View Portfolio
      </button>
    </section>

    <section class="max-w-6xl py-20 px-6 mx-auto">
      <h2 class="text-3xl font-bold mb-12 text-center" id="featured">Featured Projects</h2>
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-10" :class="featuredProjects.length > 2 && 'lg:grid-cols-3'">
        <div class="group cursor-pointer duration-200 transform hover:scale-105 rounded-2xl shadow-xl bg-white/60 backdrop-blur-md border border-gray-200 hover:border-gray-900 transition-all" v-for="project in featuredProjects" :key="project.id">
          <img class="w-full h-60 object-cover rounded-t-2xl" :src="project.image" :alt="project.name + ' thumbnail'" />
          <div class="p-6">
            <h3 class="text-lg font-semibold mb-2">{{ project.name }}</h3>
            <p class="text-sm text-gray-500 group-hover:underline">{{ project.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <section class="max-w-6xl py-20 px-6 mx-auto">
      <h2 class="text-3xl font-bold mb-12 text-center" id="featured">Latest Projects</h2>
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-10" :class="latestProjects.length > 2 && 'lg:grid-cols-3'">
        <div class="group cursor-pointer duration-200 transform hover:scale-105 rounded-2xl shadow-xl bg-white/60 backdrop-blur-md border border-gray-200 hover:border-gray-900 transition-all" v-for="project in latestProjects" :key="project.id">
          <img class="w-full h-60 object-cover rounded-t-2xl" :src="project.image" :alt="project.name + ' thumbnail'" />
          <div class="p-6">
            <h3 class="text-lg font-semibold mb-2">{{ project.name }}</h3>
            <p class="text-sm text-gray-500 group-hover:underline">{{ project.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <footer class="text-center py-12 text-sm text-gray-500">
      <div class="space-x-4">
        <a class="hover:underline" href="https://github.com/LookAtFr3sn0" target="_blank" >GitHub</a>
        <a class="hover:underline" href="https://linkedin.com/in/francescogiammari" target="_blank" >LinkedIn</a>
        <a class="hover:underline" :href="'mailto:' + 'contact' + '&commat;' + 'lookatfr3sn0.com'">Email</a>
      </div>
    </footer>
  </main>
</template>
