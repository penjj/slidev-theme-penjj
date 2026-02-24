<template>
  <div class="slidev-layout cover flex items-center justify-center">
      <AuroraBackground/>
      <div text-center>
        <slot />
      </div>
  
      <img v-if="$frontmatter.logo" class="cover-logo absolute top-14 right-14 h-10" :src="$frontmatter.logo"/>
  
      <div v-if="$frontmatter.author" class="cover-author absolute bottom-10 left-10 c-gray/30 animate-[fadeout_4s_linear_infinite]">
        @{{ $frontmatter.author }}
      </div>
    </div>
</template>

<script setup lang="ts">
import { useSlideContext } from '@slidev/client'

const { $slidev, $page, $frontmatter } = useSlideContext()
</script>
