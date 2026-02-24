<template>
  <blockquote class="quote">
    <p><slot /></p>
    <cite v-if="author">- {{ author }}</cite>
  </blockquote>
</template>

<script setup>
defineProps({
  author: String
})
</script>

<style scoped>
.quote {
  border-left: 4px solid var(--primary);
  padding-left: 1.5rem;
  margin: 2rem 0;
  font-style: italic;
}

.quote p {
  font-size: 1.5rem;
  color: var(--text-primary);
  margin: 0;
}

.quote cite {
  display: block;
  margin-top: 1rem;
  color: var(--text-secondary);
  font-size: 1rem;
}
</style>
