<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { computed } from 'vue'
import TypingStatement from './TypingStatement.vue'

defineProps<{ items: { title: string, text: string }[] }>()
const isSlideActive = useIsSlideActive()
const { $renderContext } = useSlideContext()
const animate = computed(() => isSlideActive.value
  && ($renderContext.value === 'slide' || $renderContext.value === 'presenter'))
const cardDelay = (index: number) => 180 + index * 420
</script>

<template>
  <div class="gridcards" :class="{ 'text-cards-active': animate }">
    <article v-for="(item, index) in items" :key="item.title" class="glass animated-text-card" :style="{ '--card-delay': cardDelay(index) + 'ms' }">
      <h3>{{ item.title }}</h3>
      <TypingStatement :text="item.text" :delay="cardDelay(index) + 140" plain />
    </article>
  </div>
</template>

<style scoped>
@media screen and (prefers-reduced-motion: no-preference) {
  .text-cards-active .animated-text-card {
    animation: text-card-enter 340ms ease-out var(--card-delay) backwards;
  }
}

@keyframes text-card-enter {
  from { opacity: 0; transform: translateY(12px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>
