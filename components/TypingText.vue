<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { computed } from 'vue'

const props = withDefaults(defineProps<{
  text: string
  delay?: number
  enabled?: boolean
  interval?: number
  fadeOnly?: boolean
}>(), { delay: 180, enabled: true, interval: 12 })
const isSlideActive = useIsSlideActive()
const { $renderContext } = useSlideContext()
const animate = computed(() => props.enabled && isSlideActive.value
  && ($renderContext.value === 'slide' || $renderContext.value === 'presenter'))

const tokens = computed(() => {
  let offset = 0
  return props.text.split(/(\s+)/).filter(Boolean).map(text => {
    const letters = Array.from(text)
    const token = { text, letters, offset, space: /^\s+$/.test(text) }
    offset += letters.length
    return token
  })
})
</script>

<template>
  <span :class="{ 'typing-active': animate, 'typing-fade-only': fadeOnly }">
    <span class="sr-only">{{ text }}</span>
    <span aria-hidden="true">
      <template v-for="token in tokens" :key="token.offset">
        <template v-if="token.space">{{ token.text }}</template>
        <span v-else class="typing-word"><span
          v-for="(letter, index) in token.letters"
          :key="index"
          class="typing-letter"
          :style="{ '--letter-delay': (delay + (token.offset + index) * interval) + 'ms' }"
        >{{ letter }}</span></span>
      </template>
    </span>
  </span>
</template>

<style scoped>
.typing-word { display: inline-block; white-space: nowrap; }
.typing-letter { display: inline-block; }

@media screen and (prefers-reduced-motion: no-preference) {
  .typing-active .typing-letter {
    animation: type-letter 180ms ease-out var(--letter-delay) backwards;
  }
  .typing-active.typing-fade-only .typing-letter {
    animation: type-letter-fade 90ms ease-out var(--letter-delay) backwards;
  }
}

@keyframes type-letter-fade {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes type-letter {
  from { opacity: 0; transform: translateY(5px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>

