<script setup lang="ts">
import { computed } from 'vue'
import configs from '#slidev/configs'

defineProps<{
  avatar?: string
  class?: string
}>()

const tc = computed(() => (configs as any).themeConfig ?? {})
const github = computed(() => tc.value.github ?? '')
const x = computed(() => tc.value.x ?? tc.value.twitter ?? '')
const bluesky = computed(() => tc.value.bluesky ?? '')
const linkedin = computed(() => tc.value.linkedin ?? '')
const website = computed(() => tc.value.website ?? '')
const hasSocials = computed(() => github.value || x.value || website.value)
</script>




<template>
  <div class="slidev-layout end">
    <div class="end-bg" />
    <div class="end-content">
      <slot />
      <div v-if="hasSocials" class="end-socials">
        <span v-if="bluesky">Bluesky: {{ bluesky }}</span>
        <span v-if="linkedin">LinkedIn: {{ linkedin }}</span>
        <span v-if="github">GitHub: {{ github }}</span>
        <span v-if="x">X: {{ x }}</span>
        <span v-if="website">{{ website }}</span>
      </div>
    </div>
    <div class="end-logo">
      <img src="/snyk-logo-dark.png" alt="Snyk" class="end-logo-img" />
    </div>
  </div>
</template>

<style scoped>
.end-bg {
  position: absolute;
  inset: 0;
  background: url('/bg-dots-gradient.png') no-repeat center center;
  background-size: cover;
  opacity: 0.4;
  pointer-events: none;
}

.end-content {
  z-index: 1;
}

.end-logo {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  opacity: 0.2;
  z-index: 1;
}

.end-logo-img {
  height: 28px;
  width: auto;
}

.end-socials {
  margin-top: 1rem;
  display: flex;
  gap: 1rem;
  font-size: 0.875rem;
  color: var(--snyk-text-muted);
}
</style>
<script setup lang="ts">
</script>