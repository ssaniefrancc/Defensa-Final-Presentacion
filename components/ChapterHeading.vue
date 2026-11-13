<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { computed } from 'vue'

defineProps<{ label: string, title: string }>()
const isSlideActive = useIsSlideActive()
const { $renderContext } = useSlideContext()
const reveal = computed(() => isSlideActive.value
  && ($renderContext.value === 'slide' || $renderContext.value === 'presenter'))
</script>

<template>
  <div class="chapter" :class="{ 'chapter-reveal': reveal }">
    <p class="eyebrow">{{ label }}</p>
    <h1>{{ title }}</h1>
  </div>
</template>

<style scoped>
@media screen and (prefers-reduced-motion: no-preference) {
  .chapter-reveal .eyebrow {
    animation: chapter-unfold 560ms cubic-bezier(.2,.72,.25,1) 140ms backwards;
  }

  .chapter-reveal h1 {
    animation: chapter-unfold 780ms cubic-bezier(.2,.72,.25,1) 240ms backwards;
  }
}

@keyframes chapter-unfold {
  from { clip-path: inset(-12px 50%); }
  to { clip-path: inset(-12px 0); }
}
</style>
