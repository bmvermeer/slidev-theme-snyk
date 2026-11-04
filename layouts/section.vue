<script setup lang="ts">
defineProps<{
  /** Optional full-bleed background image (with a dark overlay for text legibility). */
  bgImage?: string
}>()
</script>

<template>
  <div class="slidev-layout section">
    <template v-if="bgImage">
      <img :src="bgImage" alt="" class="section-bg" />
      <div class="section-bg-overlay" />
    </template>
    <div v-else class="section-dots" />
    <div class="section-content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.section-bg {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.section-bg-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(90deg, rgba(0, 0, 0, 0.9) 0%, rgba(0, 0, 0, 0.75) 55%, rgba(0, 0, 0, 0.55) 100%);
  pointer-events: none;
}

.section-dots {
  position: absolute;
  inset: 0;
  background: url('/bg-dots-purple.png') no-repeat right bottom;
  background-size: 50% auto;
  opacity: 0.25;
  pointer-events: none;
  -webkit-mask-image: radial-gradient(ellipse 50% 60% at 90% 85%, black 20%, transparent 70%);
  mask-image: radial-gradient(ellipse 50% 60% at 90% 85%, black 20%, transparent 70%);
}

.section-content {
  max-width: 700px;
  z-index: 1;
  position: relative;
}
</style>
