<template>
  <div class="slidev-layout two-cols-header">
    <slot/>
    <div class="grid grid-cols-2 gap-8">
      <div class="two-cols__left">
        <slot name="left" />
      </div>
      <div class="two-cols__right">
        <slot name="right" />
      </div>
    </div>
  </div>
</template>
