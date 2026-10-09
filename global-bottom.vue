<script setup lang="ts">
import { computed } from 'vue'
import { useNav } from '@slidev/client'
import { injectLocal } from '@vueuse/core'
import configs from '#slidev/configs'

const globalNav = useNav()

// In PDF/PNG export every slide is rendered at once, and PrintSlideClick provides a
// per-slide nav context. The shared useNav() follows the router instead, so it would
// report the same slide (the cover) for all pages and hide the footer everywhere.
const slideContext = injectLocal('$$slidev-context' as any, undefined) as { nav?: typeof globalNav } | undefined
const nav = computed(() => slideContext?.nav ?? globalNav)
const currentLayout = computed(() => nav.value.currentLayout)
const currentPage = computed(() => nav.value.currentPage)
const total = computed(() => nav.value.total)

const hiddenLayouts = ['cover', 'cover-alt', 'end', 'full']
const noCornerLogoLayouts = [...hiddenLayouts, 'intro']

const showSlideNumbers = computed(() => configs.themeConfig?.slideNumbers === true)

const handle = computed(() => configs.themeConfig?.handle as string | undefined)

const footerBranding = computed(() => {
  const explicit = configs.themeConfig?.footerBranding as string | undefined
  if (explicit === 'logo') return 'logo'
  if (explicit === 'handle') return handle.value ? 'handle' : 'logo'
  return handle.value ? 'handle' : 'logo'
})
</script>

<template>
  <footer v-if="!hiddenLayouts.includes(currentLayout)" class="snyk-footer">
    <div class="footer-left">
      <span v-if="footerBranding === 'handle' && handle" class="footer-handle">{{ handle }}</span>
      <img v-else src="/snyk-logo-dark.png" alt="Snyk" class="footer-logo" />
    </div>
    <div class="footer-right">
      <span v-if="showSlideNumbers">{{ currentPage }} / {{ total }}</span>
      <img
        v-if="!noCornerLogoLayouts.includes(currentLayout)"
        src="/snyk-logo-dark.png"
        alt="Snyk"
        class="footer-corner-logo"
      />
    </div>
  </footer>
</template>

<style scoped>
.snyk-footer {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.6rem 1.5rem;
  color: var(--snyk-text-muted);
  font-size: 0.7rem;
  font-family: 'Sora', sans-serif;
  pointer-events: none;
  z-index: 10;
}

.footer-left {
  opacity: 0.7np;
}

.footer-logo {
  height: 16px;
  width: auto;
}

.footer-handle {
  font-weight: 600;
  font-size: 0.75rem;
  letter-spacing: 0.02em;
}

.footer-right {
  display: flex;
  align-items: center;
  gap: 1rem;
  letter-spacing: 0.05em;
}

.footer-right span {
  opacity: 0.5;
}

.footer-corner-logo {
  height: 20px;
  width: auto;
  opacity: 0.5;
}
</style>
