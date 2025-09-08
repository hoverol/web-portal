<template>
  <div style="height:100vh; width:100vw">
    <LMap
      :zoom="11"
      :center="petropavl"
      :use-global-leaflet="false"
      style="height:100%; width:100%"
    >
      <LTileLayer
        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        attribution="&copy; OpenStreetMap contributors"
      />

      <!-- Маркер города -->
      <LMarker :lat-lng="petropavl" :draggable="false">
        <LTooltip permanent direction="top">Петропавловск (СКО)</LTooltip>
        <LPopup>Петропавловск, Северо-Казахстанская область</LPopup>
      </LMarker>

      <!-- Зафиксированные озёра -->
      <LMarker
        v-for="(lake, i) in lakes"
        :key="i"
        :lat-lng="[lake.lat, lake.lng]"
        :draggable="false"
      >
        <LTooltip permanent direction="top">{{ lake.name }}</LTooltip>
        <LPopup>
          <strong>{{ lake.name }}</strong><br />
          Координаты: {{ lake.lat }}, {{ lake.lng }}
        </LPopup>
      </LMarker>
    </LMap>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { LMap, LTileLayer, LMarker, LTooltip, LPopup } from '@vue-leaflet/vue-leaflet'
import 'leaflet/dist/leaflet.css'

type LatLngTuple = [number, number]

interface Lake {
  name: string
  lat: number
  lng: number
}

// Центр карты — Петропавловск
const petropavl = ref<LatLngTuple>([54.88, 69.16])

// Список озёр
const lakes = ref([
  { name: 'Озеро Пёстрое', lat: 54.836699, lng: 69.111382 },
  { name: 'Озеро Большое', lat: 54.927415, lng: 69.653122 },
  { name: 'Озеро Горькое', lat: 54.947573, lng: 69.951122 },
  { name: 'Озеро Солёное', lat: 54.921225, lng: 69.693476 },
  { name: 'Озеро Дикое', lat: 54.840156, lng: 69.131957 },
  { name: 'Озеро Белое', lat: 54.93405044786823, lng: 69.25532703220118 },
  { name: 'Озеро Поганка', lat: 54.922904537388504, lng: 69.05242328616905 },
  { name: 'Озеро Паганка', lat: 54.825344415110386, lng: 69.14043813009937 },
  { name: 'Озеро Гусиное', lat: 54.79330249146028, lng: 69.13763660752686 },
  { name: 'Озеро Большое Тинное', lat: 54.80383325084846, lng: 69.1554441363835 },
  { name: 'Озеро Малое Белое', lat: 54.94989945258805, lng: 69.32499451051268 },
  { name: 'Озеро Пеньковское', lat: 54.96477910906723, lng: 69.26074685992033 },
  { name: 'Озеро Киштибиш 1-й', lat: 54.96989217583696, lng: 69.17985391593116 },
  { name: 'Озеро Киштибиш 2-й', lat: 54.96150088904849, lng: 69.16200829669867 },
  { name: 'Озеро Киштибиш 3-й', lat: 54.95377729715128, lng: 69.17850876875283 },
])
</script>