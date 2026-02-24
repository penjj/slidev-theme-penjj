<template>
  <div class="slidev-layout section">
    <div class="section-content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.section {
  text-align: center;
  justify-content: center;
  align-items: center;
}

.section-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
