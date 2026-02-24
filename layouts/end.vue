<template>
  <div class="slidev-layout end flex items-center justify-center">
    <AuroraBackground/>
    <div>
      <div text-center>
        <slot />
      </div>
      <img v-if="$slidev.configs.logo" class="end-logo absolute top-14 right-14 h-10" :src="$slidev.configs.logo"/>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useSlideContext } from '@slidev/client'

const { $slidev, $page, $frontmatter } = useSlideContext()
</script>
