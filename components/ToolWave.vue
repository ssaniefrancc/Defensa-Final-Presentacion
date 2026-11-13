<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { computed } from 'vue'

const isSlideActive = useIsSlideActive()
const { $clicks, $renderContext } = useSlideContext()
const animate = computed(() => isSlideActive.value
  && ($renderContext.value === 'slide' || $renderContext.value === 'presenter'))
</script>

<template>
  <div class="tools-grid" :class="{ 'tools-wave': animate }" :data-tool-step="$clicks">
    <slot />
  </div>
</template>

<style scoped>
.tools-grid :slotted(.tool-card) {
  translate: 0 var(--tool-lift, 0);
  outline: 2px solid var(--tool-edge, transparent);
  box-shadow: var(--frost-edge), var(--tool-glow, 0 0 0 transparent);
  background: var(--tool-surface, linear-gradient(150deg, color-mix(in srgb, var(--chroma-primary) 11%, #151925), #0a0c18 92%));
}

.tools-grid[data-tool-step="1"] :slotted(.tool-card:nth-child(1)),
.tools-grid[data-tool-step="2"] :slotted(.tool-card:nth-child(2)),
.tools-grid[data-tool-step="3"] :slotted(.tool-card:nth-child(3)),
.tools-grid[data-tool-step="4"] :slotted(.tool-card:nth-child(4)),
.tools-grid[data-tool-step="5"] :slotted(.tool-card:nth-child(5)),
.tools-grid[data-tool-step="6"] :slotted(.tool-card:nth-child(6)),
.tools-grid[data-tool-step="7"] :slotted(.tool-card:nth-child(7)),
.tools-grid[data-tool-step="8"] :slotted(.tool-card:nth-child(8)) {
  --tool-edge: var(--chroma-secondary);
  --tool-glow: 0 0 26px color-mix(in srgb, var(--chroma-primary) 54%, transparent);
  --tool-lift: -7px;
  --tool-surface: linear-gradient(150deg, color-mix(in srgb, var(--chroma-primary) 36%, #151925), #101428 92%);
}

@media screen and (prefers-reduced-motion: no-preference) {
  .tools-grid :slotted(.tool-card) {
    transition: translate 220ms ease, outline-color 220ms ease, box-shadow 220ms ease;
  }

  .tools-wave[data-tool-step="0"] :slotted(.tool-card) {
    animation: tool-wave 540ms ease-in-out calc(210ms + var(--wave-order) * 105ms);
  }
}

@media (prefers-reduced-motion: reduce) {
  .tools-grid :slotted(.tool-card) { translate: none; }
}

@keyframes tool-wave {
  0%, 100% { transform: translateY(0); }
  50% {
    transform: translateY(-8px);
    box-shadow: var(--frost-edge), 0 0 24px color-mix(in srgb, var(--chroma-primary) 45%, transparent);
  }
}
</style>
