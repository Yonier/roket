<template>
  <div class="h-full flex flex-col gap-4 text-gray-600">
    <h4 class="text-lg font-bold text-black">Mapa</h4>

    <!-- Componente #1 (Lista de árboles) -->
    <template v-if="!loading">
      <div>
        Select Location<br/>
        <select
        v-model="objectId"
        class="w-full border border-gray-500 p-2 rounded text-center"
        >
          <option value="">Todos</option>
          <option v-for="(objeto, objetoIx) in objetos" :key="objetoIx" :value="objeto.object_id">
            {{ objeto.object_name }}
          </option>
        </select>
      </div>

      <div class="w-full h-[500px]">
        <!-- Componente #2 y #3 (Fotografía y Mapa árboles) -->
        <Map
        v-model:objetos="objetosActivos"
        />
      </div>
    </template>
    <template v-else>Cargando...</template>
  </div>
</template>
<script setup lang="ts">
import { computed, onMounted, ref } from 'vue';
import Map from '@/components/Map.vue';

import type { objeto } from '@/components/Map.vue';

const objectId = ref('');

const objetos = ref<objeto[]>([]);
const objetosActivos = computed(() => (
  !objectId.value ? objetos.value : objetos.value.filter(objeto => objeto.object_id === objectId.value)
));

const loading = ref(true);
onMounted(() => {
  // Obtener los objetos
  fetch('https://aqh.fitsnr.com/api/aqh/objects', {
    headers: {
      'X-token': '5Dt4y4fN1Eh8lX1cFKtO'
    }
  })
  .then(async r => {
    loading.value = false;
    objetos.value = ((await r.json()) as {
      objetos: objeto[]
    }).objetos;
  });
});
</script>
