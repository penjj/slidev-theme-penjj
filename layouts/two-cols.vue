<template>
  <div>
    <div class="slidev-layout two-cols grid grid-cols-2 gap-8">
      <div class="two-cols__left">
        <slot />
      </div>
      <div class="two-cols__right">
        <slot name="right" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useNav } from '@slidev/client'

</script>
