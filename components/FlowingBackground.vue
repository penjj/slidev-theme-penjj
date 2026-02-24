<template>
  <div
    ref="container"
    class="relative w-full h-full overflow-hidden bg-[#1e1e2e]"
  >
    <canvas
      ref="canvas"
      class="absolute top-0 left-0 w-full h-full blur-[60px]"
    ></canvas>

    <div
      class="relative z-[1] h-full flex items-center justify-center text-center bg-transparent"
    >
      <div
        class="text-[4rem] font-bold text-[var(--primary)] 
               drop-shadow-[0_0_3px_rgba(99,102,241,0.6)]
               bg-[rgba(0,0,0,0.2)] 
               px-[1rem] pt-[0.5rem] pb-[0.2em] rounded"
      >
        <slot />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted, watch } from 'vue'

const {
  colors = ['#6366f1', '#4f5f3'],
  speed = 1.5
} = defineProps<{
  colors: string[],
  speed: number
}>()

const canvas = ref<HTMLCanvasElement | null>(null)
let ctx: CanvasRenderingContext2D | null = null
let animationId: number | null = null
let time = 0

const config = computed(() => ({
  colors: colors.slice(0, 3),
  speed: speed * 0.5,
  opacity: 0.15,
  blur: 80
}))

function drawFlowingOrbs(ctx: CanvasRenderingContext2D, w: number, h: number, t: number) {
  ctx.save()
  ctx.globalCompositeOperation = 'screen'

  const orbCount = 3
  for (let i = 0; i < orbCount; i++) {
    const phase = (i / orbCount) * Math.PI * 2
    const x = w * 0.2 + Math.sin(t * 0.4 + phase) * w * 0.25 + w * 0.15
    const y = h * 0.2 + Math.cos(t * 0.4 + phase) * h * 0.2
    const size = 100 + Math.sin(t * 0.6 + phase) * w * 0.2 + w * 0.25
    const opacity = 0.15 + Math.sin(t * 0.5 + phase) * 0.15
    const color = config.value.colors[i % config.value.colors.length]

    const gradient = ctx.createRadialGradient(x, y, 0, x, y, size)
    gradient.addColorStop(0, `${color}${Math.floor(opacity * 255).toString(16).padStart(2, '0')}`)
    gradient.addColorStop(0.3, `${color}${Math.floor(opacity * 150).toString(16).padStart(2, '0')}`)
    gradient.addColorStop(0.7, `${color}${Math.floor(opacity * 80).toString(16).padStart(2, '0')}`)
    gradient.addColorStop(1, 'transparent')

    ctx.fillStyle = gradient
    ctx.beginPath()
    ctx.arc(x, y, size * 1.8, 0, Math.PI * 2)
    ctx.fill()
  }

  ctx.restore()
}

function drawWave(ctx: CanvasRenderingContext2D, w: number, h: number, t: number) {
  ctx.save()
  ctx.globalCompositeOperation = 'screen'

  const opacity = (0.08 + Math.sin(t * 0.4) * 0.08) * 0.15
  ctx.strokeStyle = config.value.colors[2 % config.value.colors.length]
  ctx.globalAlpha = opacity
  ctx.lineWidth = 2
  ctx.beginPath()
  ctx.moveTo(0, h * 0.3)
  ctx.lineTo(w, h * 0.3)
  ctx.stroke()

  ctx.restore()
}

function animate() {
  if (!ctx || !canvas.value) return

  const w = canvas.value.width
  const h = canvas.value.height

  time += 0.008 * config.value.speed

  ctx.fillStyle = '#1e1e2e'
  ctx.filter = `blur(${config.value.blur}px)`
  ctx.fillRect(0, 0, w, h)

  drawWave(ctx, w, h, time)
  drawFlowingOrbs(ctx, w, h, time)

  animationId = requestAnimationFrame(animate)
}

function handleResize() {
  if (!canvas.value) return

  const rect = canvas.value.parentElement!.getBoundingClientRect()
  const dpr = window.devicePixelRatio || 1

  canvas.value.width = rect.width * dpr
  canvas.value.height = rect.height * dpr

  if (ctx) {
    ctx.setTransform(1, 0, 0, 1, 0, 0)
    ctx.scale(dpr, dpr)
  }

  canvas.value.style.width = rect.width + 'px'
  canvas.value.style.height = rect.height + 'px'
}

onMounted(() => {
  if (!canvas.value) return
  ctx = canvas.value.getContext('2d')
  handleResize()
  animate()
  window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
  if (animationId) cancelAnimationFrame(animationId)
  window.removeEventListener('resize', handleResize)
})

watch(() => colors, handleResize, { deep: true })
</script>