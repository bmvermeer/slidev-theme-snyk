<script setup lang="ts">
defineProps<{
  /** Optional full-bleed background image (with a dark overlay for text legibility). */
  bgImage?: string
}>()
</script>

<template>
  <div class="slidev-layout default" :class="{ 'has-bg-image': bgImage }">
    <template v-if="bgImage">
      <img :src="bgImage" alt="" class="default-bg" />
      <div class="default-bg-overlay" />
    </template>
    <slot />
  </div>
</template>

<style scoped>
.has-bg-image {
  isolation: isolate;
}

.default-bg {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: -2;
}

.default-bg-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(90deg, rgba(0, 0, 0, 0.9) 0%, rgba(0, 0, 0, 0.75) 55%, rgba(0, 0, 0, 0.55) 100%);
  pointer-events: none;
  z-index: -1;
}
</style>
