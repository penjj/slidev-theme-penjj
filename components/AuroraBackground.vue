<template>
  <div
    class="absolute left-0 top-0 w-full h-full overflow-hidden z-[-1] bg-[#1e1e2e]"
  >
    <div
      v-for="(orb, index) in orbs"
      :key="index"
      :style="getOrbStyle(orb, index)"
      class="absolute rounded-full opacity-40 animate-[aurora-float_20s_ease-in-out_infinite] transform -translate-x-1/2 -translate-y-1/2"
    />
    <div class="relative z-[1]">
      <slot />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  colors: {
    type: Array,
    default: () => ['#6366f1', '#8b5cf6', '#06b6d4', '#d946ef']
  },
  speed: {
    type: Number,
    default: 1
  },
  blur: {
    type: Number,
    default: 30
  }
})

const orbs = ref([])
let animationId = null
let time = 0

function initOrbs() {
  orbs.value = props.colors.map((color, i) => ({
    x: Math.random() * 100,
    y: Math.random() * 100,
    size: 300 + Math.random() * 400,
    duration: 15 + Math.random() * 10,
    delay: Math.random() * 5
  }))
}

function getOrbStyle(orb, index) {
  return {
    background: `radial-gradient(circle, ${props.colors[index % props.colors.length]} 0%, transparent 70%)`,
    width: orb.size + 'px',
    height: orb.size + 'px',
    left: orb.x + '%',
    top: orb.y + '%',
    animationDuration: orb.duration + 's',
    animationDelay: orb.delay + 's',
    filter: `blur(${props.blur}px)`
  }
}

function animate() {
  time += 0.016 * props.speed

  orbs.value = orbs.value.map((orb, i) => {
    const phase = (i / props.colors.length) * Math.PI * 2
    const newX = 20 + Math.sin(time * 0.3 + phase + orb.delay) * 30
    const newY = 20 + Math.cos(time * 0.25 + phase + orb.delay) * 25
    return { ...orb, x: newX, y: newY }
  })

  animationId = requestAnimationFrame(animate)
}

onMounted(() => {
  initOrbs()
  animate()
})

onUnmounted(() => {
  if (animationId) cancelAnimationFrame(animationId)
})
</script>