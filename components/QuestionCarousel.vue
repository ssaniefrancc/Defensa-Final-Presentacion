<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { computed, ref, watch } from 'vue'

const props = defineProps<{
  label: string
  items: (string | { title: string, text: string })[]
}>()
const { $clicks, $renderContext } = useSlideContext()
const isSlideActive = useIsSlideActive()
const active = computed(() => Math.min(Math.max(0, $clicks.value), props.items.length - 1))
const direction = ref(1)
const unfolding = ref(false)

watch([isSlideActive, active], ([visible, step], [wasVisible, previousStep]) => {
  if (!visible || ($renderContext.value !== 'slide' && $renderContext.value !== 'presenter')) {
    unfolding.value = false
  }
  else if (!wasVisible) {
    unfolding.value = true
  }
  else if (step !== previousStep) {
    unfolding.value = false
  }
}, { immediate: true })

watch(active, (current, previous) => {
  direction.value = current > previous ? 1 : -1
}, { flush: 'sync' })

function position(index: number) {
  const length = props.items.length
  if (length === 2) return index - active.value
  const offset = (index - active.value + length) % length
  return offset > length / 2 ? offset - length : offset
}
</script>

<template>
  <div class="question-carousel" :aria-label="label">
    <div class="question-wheel" :class="{ 'carousel-unfolding': unfolding }" :style="{ '--swipe-direction': direction }">
      <article
        v-for="(item, index) in items"
        :key="typeof item === 'string' ? item : item.title"
        class="glass question-card"
        :data-position="position(index)"
        :aria-hidden="index !== active"
      >
        <span class="question-number">{{ index + 1 }}</span>
        <div class="question-content">
          <slot :name="'item-' + index">
            <h2 v-if="typeof item !== 'string'">{{ item.title }}</h2>
            <p>{{ typeof item === 'string' ? item : item.text }}</p>
          </slot>
        </div>
      </article>
    </div>
    <p class="question-progress" aria-live="polite">{{ active + 1 }} / {{ items.length }}</p>
  </div>
</template>

<style scoped>
.question-carousel {
  display: grid;
  gap: 22px;
  width: 100%;
}

.question-wheel {
  position: relative;
  isolation: isolate;
  height: 370px;
  perspective: 1050px;
}

.question-carousel .question-card {
  position: absolute;
  inset: 0;
  display: grid;
  place-items: center;
  width: min(75%, 830px);
  margin-inline: auto;
  padding: 26px 58px;
  border: 1px solid var(--line);
  background: linear-gradient(145deg, #232344, #101122 85%);
  opacity: .62;
  text-align: center;
}

.question-content {
  display: grid;
  justify-items: center;
  gap: 13px;
}

.question-number {
  position: absolute;
  top: 24px;
  left: 28px;
  display: grid;
  place-items: center;
  width: 38px;
  height: 38px;
  border: 1px solid var(--line);
  border-radius: 50%;
  background: var(--wash);
  color: var(--chroma-highlight);
  font: 500 22px var(--display);
}

.question-card p {
  color: var(--ice);
  font-size: 30px;
  line-height: 1.42;
  text-wrap: balance;
}

.question-card h2 {
  margin: 0;
  color: var(--chroma-highlight);
  font: 500 36px/1.2 var(--display);
}

.question-carousel .question-card[data-position="0"] {
  z-index: 3;
  opacity: 1;
  transform: translateX(0);
  border-color: color-mix(in srgb, var(--chroma-secondary) 44%, transparent);
}

.question-card[data-position="-1"] {
  z-index: 2;
  transform: translateX(-164px) rotateY(18deg) rotateZ(-4deg) scale(.87);
}

.question-card[data-position="1"] {
  z-index: 2;
  transform: translateX(164px) rotateY(-18deg) rotateZ(4deg) scale(.87);
}

.question-carousel .question-card[data-position="2"] {
  z-index: 1;
  opacity: .4;
  transform: translateX(230px) rotateY(-24deg) rotateZ(7deg) scale(.74);
}

.question-carousel .question-card[data-position="-2"] {
  z-index: 1;
  opacity: .4;
  transform: translateX(-230px) rotateY(24deg) rotateZ(-7deg) scale(.74);
}

.question-carousel .question-card[data-position="3"] {
  z-index: 0;
  opacity: .28;
  transform: translateX(260px) rotateY(-27deg) rotateZ(9deg) scale(.63);
}

.question-carousel .question-card[aria-hidden="true"] :is(h2, p) {
  visibility: hidden;
}

.question-card[aria-hidden="true"][data-position^="1"] .question-number,
.question-card[aria-hidden="true"][data-position="2"] .question-number,
.question-card[aria-hidden="true"][data-position="3"] .question-number {
  left: auto;
  right: 28px;
}

.question-progress {
  color: var(--chroma-highlight);
  font-size: 20px;
  text-align: center;
  font-variant-numeric: tabular-nums;
}

@media screen and (prefers-reduced-motion: no-preference) {
  .question-carousel .question-card {
    transition: transform 550ms cubic-bezier(.2,.72,.25,1), opacity 420ms ease, border-color 420ms ease;
  }

  .question-card[data-position="0"] .question-content {
    animation: question-swipe 460ms cubic-bezier(.2,.72,.25,1) both;
  }

  .carousel-unfolding .question-card[aria-hidden="true"] {
    animation: carousel-unfold 760ms cubic-bezier(.2,.72,.25,1) 170ms backwards;
  }
}

@keyframes carousel-unfold {
  from { transform: translateX(0) scale(.98); }
}

@keyframes question-swipe {
  from {
    opacity: 0;
    transform: translateX(calc(var(--swipe-direction) * 110px));
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}
</style>
