<template>
  <div class="slidev-layout fact">
    <div class="fact-content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.fact-content {
  max-width: 600px;
}

.slidev-layout.fact .fact-content :deep(h1) {
  font-size: 3rem;
}

.slidev-layout.fact .fact-content :deep(h2) {
  font-size: 1.4rem;
}

.slidev-layout.fact .fact-content :deep(p) {
  font-size: 1rem;
}
</style>
