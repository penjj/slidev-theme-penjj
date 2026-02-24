<template>
  <div>
    <div class="slidev-layout">
      <slot />
    </div>
  </div>
</template>

<script setup lang="ts">
import { useSlideContext } from '@slidev/client'
import { unref } from 'vue';

const { $slidev, $page, $frontmatter } = useSlideContext()
</script>
