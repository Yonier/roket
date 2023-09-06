<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router';
import IconTree from './components/icon/Tree.vue';
</script>

<template>
  <div
  class="
  bg-gradient-to-l from-green-100 to-white-500
  w-full min-h-screen max-h-screen flex justify-center align-center p-8
  "
  >
    <div class="m-auto gap-4 w-full md:w-[50%] h-[50%]">
      <header class="w-full text-center text-3xl font-bold mb-4">
        <IconTree :size="70" class="d-block m-auto text-green-500"/>
        Roket
        <nav class="text-center text-sm flex justify-center gap-2 font-normal">
          <RouterLink to="/" activeClass="text-green-600 font-bold">Inicio</RouterLink>
          | <RouterLink to="/map" activeClass="text-green-600 font-bold">Mapa</RouterLink>
        </nav>
      </header>

      <main class="border border-gray-100 bg-white w-full h-full p-4 rounded-lg">
        <RouterView  v-slot="{ Component }">
          <transition
          enterFromClass="opacity-0"
          enterActiveClass="transition duration-300"
          >
            <component :is="Component" />
          </transition>
        </RouterView>
      </main>
    </div>
  </div>
</template>