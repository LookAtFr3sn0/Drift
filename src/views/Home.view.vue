<script setup>
import { ref, computed, onMounted, nextTick } from 'vue';
import gsap from 'gsap';
import scrollTo from '@/utils/scrollTo.js';
import projects from '/src/assets/projects.json';

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

onMounted(async () => {
  await nextTick();
  gsap.from('.floating-shape', {
    opacity: 0,
    scale: 0.7,
    stagger: 0.2,
    duration: 1.2,
    delay: 0.2,
    ease: 'back.out(1.7)',
  });
})
</script>

<template>
  <main class="w-full min-h-screen text-gray-900 font-mono bg-gradient-to-r from-blue-100 via-purple-100 to-pink-100 relative">

    <div class="pointer-events-none inset-0 z-0">
      <span class="floating-shape bg-gradient-to-br from-blue-300/60 via-cyan-300/40 to-green-200/40 top-[10%] left-[15%] w-20 h-20 animate-color-splash"></span>
      <span class="floating-shape bg-gradient-to-br from-pink-300/60 via-fuchsia-300/40 to-purple-200/40 top-[60%] left-[80%] w-14 h-14 animate-color-splash" style="animation-delay: 2s;"></span>
      <span class="floating-shape bg-gradient-to-br from-purple-300/60 via-indigo-300/40 to-blue-200/40 top-[30%] left-[60%] w-24 h-24 animate-color-splash" style="animation-delay: 4s;"></span>
      <span class="floating-shape bg-gradient-to-br from-yellow-200/60 via-orange-200/40 to-pink-200/40 top-[80%] left-[10%] w-16 h-16 animate-color-splash" style="animation-delay: 1.5s;"></span>
    </div>

    <section class="h-screen flex flex-col items-center justify-center text-center px-6 relative bg-gradient-to-b from-black/5 via-transparent to-transparent">
      <h1 class="text-6xl md:text-8xl font-semibold drop-shadow-lg mb-4 select-none animate-fade-in bg-gradient-to-r from-blue-500 via-purple-400 to-pink-400 bg-clip-text text-transparent" id="title">LookAtFr3sn0</h1>
      <div class="flex gap-4 text-sm md:text-lg lg:text-xl text-gray-600 mb-8 items-center justify-center" id="subtitle">
        <p class="animate-fade-in opacity-0">Software developer</p>
        <span class="animate-fade-in opacity-0 h-4 w-px rounded-full bg-gray-400 inline-block"></span>
        <p class="animate-fade-in opacity-0">Game developer</p>
        <span class="animate-fade-in opacity-0 h-4 w-px rounded-full bg-gray-400 inline-block"></span>
        <p class="animate-fade-in opacity-0">3D artist</p>
      </div>
      <button
        class="animate-fade-in opacity-0 cursor-pointer border border-gray-900 px-6 py-2 text-sm uppercase tracking-widest rounded-full bg-white/40 backdrop-blur-md shadow-md hover:bg-gray-900 hover:text-white transition-all duration-200 font-semibold select-none"
        id="portfolio-button"
        @click="scrollTo('skills')"
      >
        View Portfolio
      </button>
    </section>

    <section class="max-w-6xl py-20 px-6 mx-auto">
      <h2 class="text-3xl font-bold mb-12 text-center" id="skills">Skills & Technologies</h2>
      <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-8 text-center *:*:first:select-none">
        <div class="flex flex-col items-center">
            <img class="w-10 h-10 mb-2" src="/src/assets/vue.svg" alt="Vue.js logo" />
          <span class="font-semibold">Vue.js</span>
        </div>
        <div class="flex flex-col items-center">
          <img class="w-10 h-10 mb-2" src="/src/assets/react.svg" alt="React logo" />
          <span class="font-semibold">React</span>
        </div>
        <div class="flex flex-col items-center">
          <img class="w-10 h-10 mb-2" src="/src/assets/tailwind.svg" />
          <span class="font-semibold">TailwindCSS</span>
        </div>
        <div class="flex flex-col items-center">
          <img class="w-10 h-10 mb-2" src="/src/assets/ts.svg" alt="TypeScript logo" />
          <span class="font-semibold">TypeScript</span>
        </div>
        <div class="flex flex-col items-center">
          <img class="w-10 h-10 mb-2" src="/src/assets/node.svg" />
          <span class="font-semibold">Node.js</span>
        </div>
        <div class="flex flex-col items-center">
          <img class="w-10 h-10 mb-2" src="/src/assets/postgres.svg" alt="PostgreSQL logo" />
          <span class="font-semibold">PostgreSQL</span>
        </div>
        <div class="flex flex-col items-center">
          <img class="w-10 h-10 mb-2" src="/src/assets/blender.png" alt="Blender logo" />
          <span class="font-semibold">Blender</span>
        </div>
      </div>
    </section>

    <section class="max-w-6xl py-20 px-6 mx-auto" v-if="featuredProjects.length > 0">
      <h2 class="text-3xl font-bold mb-12 text-center" id="featured">Featured Projects</h2>
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-10" :class="featuredProjects.length > 2 && 'lg:grid-cols-3'">
        <div class="group cursor-pointer duration-200 transform hover:scale-105 rounded-2xl shadow-xl bg-white/60 backdrop-blur-md border border-gray-200 hover:border-gray-900 transition-all" v-for="project in featuredProjects" :key="project.id">
          <img class="w-full h-60 object-fit rounded-t-2xl" :src="project.image" :alt="project.name + ' thumbnail'" />
          <div class="p-6">
            <h3 class="text-lg font-semibold mb-2">{{ project.name }}</h3>
            <p class="text-sm text-gray-500 group-hover:underline">{{ project.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <section class="max-w-6xl py-20 px-6 mx-auto" v-if="latestProjects.length > 0">
      <h2 class="text-3xl font-bold mb-12 text-center" id="featured">Latest Projects</h2>
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-10" :class="latestProjects.length > 2 && 'lg:grid-cols-3'">
        <div class="group cursor-pointer duration-200 transform hover:scale-105 rounded-2xl shadow-xl bg-white/60 backdrop-blur-md border border-gray-200 hover:border-gray-900 transition-all" v-for="project in latestProjects" :key="project.id">
          <img class="w-full h-60 object-fit rounded-t-2xl" :src="project.image" :alt="project.name + ' thumbnail'" />
          <div class="p-6">
            <h3 class="text-lg font-semibold mb-2">{{ project.name }}</h3>
            <p class="text-sm text-gray-500 group-hover:underline">{{ project.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <footer class="text-center py-12 text-sm text-gray-500">
      <div class="flex gap-4 items-center justify-center *:hover:underline">
        <a href="https://github.com/LookAtFr3sn0/Drift" target="_blank">Source</a>
        <a href="https://github.com/LookAtFr3sn0" target="_blank" >GitHub</a>
        <a href="https://linkedin.com/in/francescogiammari/" target="_blank" >LinkedIn</a>
        <a :href="'mailto:' + 'contact' + '&commat;' + 'lookatfr3sn0.com'">Email</a>
      </div>
    </footer>
  </main>
</template>

<style scoped>
.floating-shape {
  @apply rounded-full blur-[4px] absolute;
  animation: float 8s ease-in-out infinite alternate;
}

@keyframes float {
  from { transform: translateY(0) scale(1);}
  to { transform: translateY(-30px) scale(1.08);}
}
</style>