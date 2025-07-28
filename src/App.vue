<script setup lang="ts">
import { onMounted, onUnmounted, ref } from "vue";
import { useDark, useToggle } from "@vueuse/core";
import type { ComponentPublicInstance } from "vue";
import type { IComponentCesiumMapExpose } from "./types/CesiumMap";

import CesiumMap from "./components/CesiumMap.vue";

const cesiumMapRef = ref<ComponentPublicInstance<IComponentCesiumMapExpose> | null>(null);
const hideMap = ref<boolean>(false);

const isDark = useDark({
  selector: "html",
  attribute: "data-theme",
  valueDark: "dark",
  valueLight: "light",
});

const toggleDark = useToggle(isDark);

const toggleMap = () => (hideMap.value = !hideMap.value);



onMounted(() => {
});

onUnmounted(() => {
});
</script>

<template>
  <div class="w-full h-screen overflow-hidden">
    <CesiumMap ref="cesiumMapRef" v-show="!hideMap" />

    <div class="absolute bottom-2.5 right-2.5 z-50 flex flex-col gap-2 min-w-40">
      <button v-show="!hideMap"
        class="w-full border p-4 cursor-pointer rounded-md transition text-white bg-sky-900 hover:bg-sky-700"
        @click="cesiumMapRef?.focusOnWaypointById('5')">
        🔍 Go to Waypoint 5
      </button>

      <button class="w-full border p-4 cursor-pointer rounded-md transition text-white bg-sky-900 hover:bg-sky-700"
        @click="toggleDark()">
        Switch to {{ !isDark ? "🌙" : "☀️" }}
      </button>

      <button class="w-full border p-4 cursor-pointer rounded-md transition text-white bg-sky-900 hover:bg-sky-700"
        @click="toggleMap()">
        {{ !hideMap ? "👁️ Show Map" : "🚫 Hide Map" }}
      </button>
    </div>
  </div>
</template>
