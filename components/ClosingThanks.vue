<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { computed } from 'vue'

const title = 'GRACIAS POR SU ATENCIÓN'
const words = title.split(' ')
const isSlideActive = useIsSlideActive()
const { $renderContext } = useSlideContext()
const animate = computed(() => isSlideActive.value
  && ($renderContext.value === 'slide' || $renderContext.value === 'presenter'))
</script>

<template>
  <div class="chapter closing-slide" :class="{ 'closing-active': animate }">
    <h1 :aria-label="title">
      <span v-for="(word, index) in words" :key="word" class="closing-word" :style="{ '--word-delay': (180 + index * 110) + 'ms' }" aria-hidden="true">{{ word }}</span>
    </h1>
    <div class="cover-spectrum closing-spectrum" aria-hidden="true">
      <i v-for="index in 6" :key="index" :style="{ '--swatch-delay': (670 + (index - 1) * 85) + 'ms' }" />
    </div>
    <p class="lead closing-prompt">¿Preguntas o comentarios?</p>
  </div>
</template>

<style scoped>
.closing-slide h1 {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: .24em;
}

.closing-word {
  display: inline-block;
  background: var(--skywash);
  background-clip: text;
  color: transparent;
}

.closing-slide .closing-spectrum { margin-top: 27px; }
.closing-slide .closing-prompt { margin-top: 28px; }

@media screen and (prefers-reduced-motion: no-preference) {
  .closing-active .closing-word {
    animation: closing-word-in 590ms cubic-bezier(.18,.72,.22,1) var(--word-delay) backwards;
  }

  .closing-active .closing-spectrum i {
    animation: closing-swatch-light 650ms ease-out var(--swatch-delay) backwards;
  }

  .closing-active .closing-prompt {
    animation: closing-prompt-in 540ms ease-out 1180ms backwards;
  }
}

@keyframes closing-word-in {
  from { opacity: 0; transform: translateY(25px); filter: blur(7px); }
  to { opacity: 1; transform: translateY(0); filter: blur(0); }
}

@keyframes closing-swatch-light {
  0% { opacity: 0; transform: scaleX(.25); }
  40% { opacity: 1; transform: scaleX(1); box-shadow: 0 0 24px var(--chroma-primary), 0 0 8px var(--swatch); }
  100% { opacity: 1; transform: scaleX(1); box-shadow: 0 0 0 transparent; }
}

@keyframes closing-prompt-in {
  from { opacity: 0; transform: translateY(8px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>
