<template>
  <div class="w-full h-full">
    <LMap
      :zoom="2"
      :center="[47.41322, -1.219482]"
      :useGlobalLeaflet="false"
    >
      <LTileLayer
        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
      ></LTileLayer>

      <LMarker
      v-for="objeto in objetos"
      :lat-lng="[Number(objeto.lat), Number(objeto.lon)]"
      >
        <LPopup
        :options="{
          minWidth: 200,
        }"
        >
          <img
          :src="objeto.image_url"
          width="200"
          height="50"
          />
        </LPopup>
      </LMarker>
    </LMap>
  </div>
</template>
<script setup lang="ts">
import {
  LMap,
  LTileLayer,
  LMarker,
  LPopup,
} from "@vue-leaflet/vue-leaflet";
import "leaflet/dist/leaflet.css";

export type objeto = {
  image_url: string
  lat: string
  lon: string
  location: string
  nickname: string
  nuberef: string
  object_id: string
  object_name: string
};

const props = defineProps<{
  objetos: objeto[]
}>();

</script>
