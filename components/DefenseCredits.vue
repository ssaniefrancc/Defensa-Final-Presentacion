<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { computed } from 'vue'

defineProps<{
  authors: { given: string, family: string }[]
  tutor: string
}>()
const isSlideActive = useIsSlideActive()
const { $renderContext } = useSlideContext()
const reveal = computed(() => isSlideActive.value
  && ($renderContext.value === 'slide' || $renderContext.value === 'presenter'))
</script>

<template>
  <div class="glass defense-credits" :class="{ 'credits-reveal': reveal }">
    <ul class="credit-authors" aria-label="Autores">
      <li
        v-for="(author, index) in authors"
        :key="author.family"
        class="credit-person"
        :style="{ '--credit-delay': (180 + index * 300) + 'ms' }"
      >
        {{ author.given }}<br>{{ author.family }}
      </li>
    </ul>
    <div class="credit-person credit-tutor" :style="{ '--credit-delay': (180 + authors.length * 300) + 'ms' }">
      <p class="credit-role">Tutor</p>
      <p class="credit-name">{{ tutor }}</p>
    </div>
  </div>
</template>

<style scoped>
.defense-credits {
  align-self: center;
  width: min(100%, 900px);
  padding: 45px 54px 39px;
  text-align: center;
}

.credit-authors {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 32px;
  margin: 0;
  padding: 0;
  list-style: none;
  color: var(--ice);
  font: 500 31px/1.26 var(--display);
}

.credit-tutor {
  width: min(100%, 520px);
  margin: 33px auto 0;
  padding-top: 24px;
  border-top: 1px solid var(--line);
}

.credit-role {
  color: var(--muted);
  font-size: 15px;
  letter-spacing: .14em;
  text-transform: uppercase;
}

.credit-tutor .credit-name {
  margin-top: 8px;
  color: var(--ice);
  font: 500 26px/1.25 var(--display);
}

@media screen and (prefers-reduced-motion: no-preference) {
  .credits-reveal .credit-person {
    animation: credit-appear 330ms ease-out var(--credit-delay) backwards;
  }
}

@keyframes credit-appear {
  from { opacity: 0; transform: translateY(9px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>
