<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  columns?: number
  gap?: string
}>()

const gridClass = computed(() => {
  const cols = props.columns || 3
  return `grid-cols-${cols}`
})
</script>

<template>
  <div class="slidev-layout flex flex-col h-full p-8">
    <div class="mb-6">
      <slot name="header" />
    </div>

    <div
      class="grid items-stretch content-start gap-6"
      :class="[gridClass]"
    >
      <slot name="list" />
    </div>

    <div class="mt-6">
      <slot name="footer" />
    </div>
  </div>
</template>

<style scoped>
:deep(h1) {
  --at-apply: text-3xl font-bold m-0;
}

:deep(h2) {
  --at-apply: text-xl font-semibold m-0 text-gray-400;
}

:deep(.grid > *) {
  --at-apply: p-6 rounded-xl transition-all duration-300 ease-out;
  --at-apply: bg-gradient-to-br from-blue-500/10 to-purple-600/10;
  --at-apply: border border-white/10;
  --at-apply: h-full flex flex-col;
}

:deep(.grid > *:hover) {
  --at-apply: border-blue-500/50 -translate-y-1;
  box-shadow: 0 10px 40px -10px rgba(59, 130, 246, 0.3);
}

:deep(.grid > * h2) {
  --at-apply: text-lg font-semibold mb-3 text-blue-400 m-0;
}

:deep(.grid > * p) {
  --at-apply: m-0 leading-relaxed text-gray-300;
}
</style>
