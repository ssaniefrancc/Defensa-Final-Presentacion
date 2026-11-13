<script setup lang="ts">
import { useSlideContext } from '@slidev/client'

const { $page } = useSlideContext()
</script>

<template>
  <span class="slide-number" :aria-label="'Diapositiva ' + $page">{{ $page }}</span>
</template>

<style scoped>
.slide-number {
  position: absolute;
  right: 26px;
  bottom: 19px;
  z-index: 3;
  color: #c7d3ea;
  font: 500 13px/1 var(--sans);
  font-variant-numeric: tabular-nums;
  pointer-events: none;
}

@media screen {
  .slidev-page:has(.cover-waiting) .slide-number { visibility: hidden; }
}
</style>
