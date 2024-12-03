<template>
  <header>
    <Tabs :tabs="tabs" v-model="currentTabIndex" />
  </header>

  <main>
    <div v-if="currentTab" :key="currentTabIndex">
      <h2>{{ currentTab.title }}</h2>

      <!-- :src="`http://localhost:5173/video/${currentTab.param}`"  -->
      <div class="sizes">
        <div class="size" v-for="(size, sizeIndex) in sizes" :key="sizeIndex">
          <p>
            {{ size }}
          </p>

          <iframe
            :width="size.width"
            :height="size.height"
            :src="`https://video.sevenmediaviewer.com/video/${currentTab.param}`"
            frameborder="0"
          ></iframe>
        </div>
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
  lg: { width: 400, height: 400 },
  xl: { width: 500, height: 500 },
})

const currentTabIndex = ref('')

const currentTab = computed(() => tabs.value[currentTabIndex.value])
</script>

<style scoped>
header {
  line-height: 1.5;
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
</style>
