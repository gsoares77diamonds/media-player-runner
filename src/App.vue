<template>
  <header>
    <Tabs :tabs="tabs" v-model="currentTabIndex" />

    <div>
      <label for="size-selector">Sizes:</label>
      <select v-model="currentSize" id="size-selector">
        <option v-for="(size, sizeIndex) in sizes" :key="sizeIndex" :value="sizeIndex">
          {{ sizeIndex }} - {{ size }}
        </option>
      </select>
    </div>
  </header>

  <main>
    <div v-if="currentTab" :key="currentTabIndex">
      <h2>{{ currentTab.title }}</h2>

      <!-- :src="`http://localhost:5173/video/${currentTab.param}`"  -->
      <div class="sizes">
        <iframe
          :key="currentSize"
          :width="sizes[currentSize].width"
          :height="sizes[currentSize].height"
          :src="`https://video.sevenmediaviewer.com/video/${currentTab.param}`"
          frameborder="0"
        ></iframe>
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref, computed } from 'vue'

import Tabs from './components/Tabs.vue'

// JSON: https://video.sevenmediaviewer.com/video/RBJVBUA5KDB
// ImageSet: https://video.sevenmediaviewer.com/video/RBOZKCLKOJEX
// HTML: https://video.sevenmediaviewer.com/video/OVPUIFSHMVTGBUE

const tabs = ref([
  { title: 'JSON', param: 'RBJVBUA5KDB ' },
  { title: 'Image', param: 'RBOZKCLKOJEX' },
  { title: 'HTML', param: 'OVPUIFSHMVTGBUE' },
])

const sizes = ref({
  sm: { width: 200, height: 200 },
  md: { width: 300, height: 150 },
  md1: { width: 350, height: 350 },
  lg: { width: 400, height: 400 },
  xl: { width: 500, height: 500 },
})

const currentSize = ref('sm')
const currentTabIndex = ref('')

const currentTab = computed(() => tabs.value[currentTabIndex.value])
</script>

<style scoped>
header {
  line-height: 1.5;
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}

.sizes {
  display: flex;
  justify-content: center;
}
</style>
