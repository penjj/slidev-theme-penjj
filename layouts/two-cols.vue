<template>
  <div class="slidev-layout two-cols grid grid-cols-2 gap-8 h-full of-y-hidden">
    <div class="two-cols__left h-full of-y-scroll">
      <slot />
    </div>
    <div class="two-cols__right h-full of-y-scroll">
      <slot name="right" />
    </div>
  </div>
</template>
