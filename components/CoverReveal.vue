<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { computed } from 'vue'

const isSlideActive = useIsSlideActive()
const { $clicks, $renderContext } = useSlideContext()
const interactive = computed(() => $renderContext.value === 'slide' || $renderContext.value === 'presenter')
const revealed = computed(() => !interactive.value || $clicks.value > 0)
const pulse = computed(() => interactive.value && isSlideActive.value && revealed.value)
</script>

<template>
  <main class="frame cover-reveal" :class="{ 'cover-waiting': !revealed, 'cover-pulsing': pulse }">
    <slot />
    <div class="cover-gray-veil" aria-hidden="true" />
    <div class="cover-color-pulse" aria-hidden="true" />
  </main>
</template>

<style scoped>
@property --cover-color-radius {
  syntax: '<percentage>';
  inherits: false;
  initial-value: 0%;
}

.cover-reveal {
  --pulse-origin: 50% 38%;
  --pulse-delay: 850ms;
  --pulse-duration: 900ms;
}

.cover-gray-veil,
.cover-color-pulse {
  position: absolute;
  inset: 0;
  z-index: 2;
  opacity: 0;
  pointer-events: none;
}

.cover-gray-veil { backdrop-filter: grayscale(1); }

.cover-color-pulse {
  background:
    repeating-linear-gradient(90deg, #98c0ef50 0 1px, transparent 1px 80px),
    repeating-linear-gradient(0deg, #b49afb45 0 1px, transparent 1px 80px);
  background-position: left top;
  mix-blend-mode: screen;
}

@media screen {
  .cover-waiting .cover-gray-veil { opacity: 1; }
  .cover-waiting :slotted(.hero) :is(.cover-copy, .wordmark) { visibility: hidden; }
  .cover-waiting :slotted(.hero) .cover-spectrum,
  .cover-waiting :slotted(.cover-university) { visibility: hidden; }
}

@media screen and (prefers-reduced-motion: no-preference) {
  .cover-pulsing .cover-gray-veil {
    mask-image: radial-gradient(ellipse farthest-corner at var(--pulse-origin),
      transparent var(--cover-color-radius), #000 calc(var(--cover-color-radius) + 28%));
    animation: cover-color-unfold var(--pulse-duration) cubic-bezier(.22,.61,.36,1) var(--pulse-delay) both;
  }
  .cover-pulsing .cover-color-pulse {
    mask-image: radial-gradient(ellipse farthest-corner at var(--pulse-origin),
      transparent calc(var(--cover-color-radius) - 9%),
      #000 calc(var(--cover-color-radius) + 7%),
      transparent calc(var(--cover-color-radius) + 30%));
    animation: cover-palette-pulse var(--pulse-duration) cubic-bezier(.22,.61,.36,1) var(--pulse-delay) both;
  }
  .cover-pulsing :slotted(.hero) .wordmark {
    animation:
      cover-text-unfold 340ms cubic-bezier(.2,.72,.25,1) backwards,
      cover-wordmark-in 280ms ease-out backwards,
      cover-wordmark-charge 640ms ease-in-out calc(var(--pulse-delay) - 320ms) backwards;
  }
  .cover-pulsing :slotted(.hero) .cover-copy {
    animation: cover-text-unfold 380ms cubic-bezier(.2,.72,.25,1)
      calc(var(--pulse-delay) + var(--copy-delay)) backwards;
  }
  .cover-pulsing :slotted(.hero) .cover-spectrum {
    animation: cover-detail-in 300ms ease-out calc(var(--pulse-delay) + 230ms) backwards;
  }
  .cover-pulsing :slotted(.cover-university) {
    animation: cover-detail-in 320ms ease-out calc(var(--pulse-delay) + 400ms) backwards;
  }
}

@keyframes cover-detail-in {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}

@keyframes cover-text-unfold {
  from { clip-path: inset(-55px 50%); }
  to { clip-path: inset(-55px 0); }
}

@keyframes cover-color-unfold {
  from { --cover-color-radius: -28%; opacity: 1; }
  to { --cover-color-radius: 104%; opacity: 1; }
}

@keyframes cover-palette-pulse {
  0% { --cover-color-radius: -28%; opacity: 0; }
  32% { opacity: .9; }
  100% { --cover-color-radius: 104%; opacity: 0; }
}

@keyframes cover-wordmark-in {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes cover-wordmark-charge {
  0%, 100% {
    transform: scale(1);
    filter: brightness(1) drop-shadow(0 0 8px transparent)
      drop-shadow(0 0 32px color-mix(in srgb, var(--chroma-primary) 46%, transparent));
  }
  50% {
    transform: scale(1.022);
    filter: brightness(1.3) drop-shadow(0 0 19px #fffa)
      drop-shadow(0 0 48px var(--chroma-primary));
  }
}
</style>
