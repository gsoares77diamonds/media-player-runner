<template>
  <div class="tabs">
    <button
      class="tabs__tab"
      v-for="(tab, tabIndex) in tabs"
      :key="tabIndex"
      @click="handleClick(tabIndex)"
    >
      {{ tab.title }}
    </button>
  </div>
</template>

<script setup>
import { onMounted, ref, watch } from 'vue'
const props = defineProps({
  tabs: {
    type: Array,
    required: true,
  },
  modelValue: {
    type: String,
    default: null,
  },
})

const currentTab = ref('')
const emits = defineEmits(['update:modelValue'])

watch(
  () => props.modelValue,
  () => {
    currentTab.value = props.modelValue
  },
)

watch(
  () => currentTab.value,
  () => {
    emits('update:modelValue', currentTab.value)
  },
)

function handleClick(tabIndex) {
  currentTab.value = tabIndex
}

onMounted(() => {
  if (!props.modelValue) {
    currentTab.value = 0
  }
})
</script>

<style scoped>
.tabs {
  display: flex;
  gap: 15px;
}

.tabs .tabs__tab {
}
</style>
