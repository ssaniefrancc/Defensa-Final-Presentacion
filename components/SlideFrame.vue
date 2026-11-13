<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { computed } from 'vue'

const isSlideActive = useIsSlideActive()
const { $renderContext } = useSlideContext()
const animate = computed(() =>
  isSlideActive.value &&
  ($renderContext.value === 'slide' || $renderContext.value === 'presenter')
)
</script>

<template>
  <main class="frame" :class="{ 'slide-frame-active': animate }">
    <slot />
  </main>
</template>

<style>
/*
 * Entrance animation for direct .glass children inside an active SlideFrame.
 * Each card gets a staggered delay via its --card-order custom property
 * (0-based index set inline in slides.md). Falls back to order 0 if unset.
 *
 * Usage in slides.md:
 *   <SlideFrame>
 *     <h1 class="slide-title">…</h1>
 *     <div class="glass" style="--card-order:0">…</div>
 *     <div class="glass" style="--card-order:1">…</div>
 *   </SlideFrame>
 *
 * When all children share one wrapper (.gridcards, .glass, etc.) that wrapper
 * itself can carry --card-order:0 to animate as a single unit.
 */
@media screen and (prefers-reduced-motion: no-preference) {
  .slide-frame-active .glass {
    animation: slide-frame-card-in 420ms ease-out
      calc(140ms + var(--card-order, 0) * 130ms) backwards;
  }
}

@keyframes slide-frame-card-in {
  from { opacity: 0; transform: translateY(14px); }
  to   { opacity: 1; transform: translateY(0); }
}
</style>
