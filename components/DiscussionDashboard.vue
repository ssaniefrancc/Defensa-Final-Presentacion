<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { useMediaQuery } from '@vueuse/core'
import { computed, ref, watch } from 'vue'

const props = defineProps<{
  metrics: { value: number, stage: string, description: string }[]
}>()

const isSlideActive = useIsSlideActive()
const { $renderContext } = useSlideContext()
const allowMotion = useMediaQuery('screen and (prefers-reduced-motion: no-preference)')
const animate = computed(() => allowMotion.value && isSlideActive.value
  && ($renderContext.value === 'slide' || $renderContext.value === 'presenter'))
const elapsed = ref<number | null>(null)
const duration = 700
const delay = (index: number) => 180 + index * 160

watch(animate, (active, _, onCleanup) => {
  elapsed.value = active ? 0 : null
  if (!active) return

  const start = performance.now()
  const end = delay(props.metrics.length - 1) + duration
  let frame = requestAnimationFrame(tick)
  function tick(now: number) {
    const time = now - start
    elapsed.value = time < end ? time : null
    if (elapsed.value !== null) frame = requestAnimationFrame(tick)
  }
  onCleanup(() => cancelAnimationFrame(frame))
}, { immediate: true })

function currentValue(value: number, index: number) {
  if (elapsed.value === null) return value
  const progress = Math.max(0, Math.min(1, (elapsed.value - delay(index)) / duration))
  return Math.round(value * (1 - (1 - progress) ** 3))
}
</script>

<template>
  <div class="discussion-dashboard" :class="{ 'discussion-active': animate }">
    <div class="discussion-metrics">
      <article
        v-for="(metric, index) in metrics"
        :key="metric.description"
        class="glass discussion-card"
        :style="{ '--card-delay': delay(index) + 'ms', '--current-value': currentValue(metric.value, index) + '%' }"
      >
        <p class="discussion-stage">{{ metric.stage }}</p>
        <strong class="discussion-value">
          <span class="sr-only">{{ metric.value }} %</span>
          <span aria-hidden="true">{{ currentValue(metric.value, index) }} %</span>
        </strong>
        <p class="discussion-description">{{ metric.description }}</p>
        <div class="discussion-track" aria-hidden="true"><div /></div>
      </article>
    </div>
  </div>
</template>

<style scoped>
.discussion-dashboard {
  width: 100%;
}
.discussion-metrics {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 18px;
}
.discussion-metrics .discussion-card {
  display: grid;
  grid-template-rows: auto auto 1fr auto;
  gap: 15px;
  min-width: 0;
  padding: 25px 27px;
}
.discussion-stage {
  color: var(--muted);
  font-size: 16px;
}
.discussion-value {
  color: var(--chroma-highlight);
  font: 500 66px/1 var(--display);
  font-variant-numeric: tabular-nums;
  white-space: nowrap;
}
.discussion-description {
  color: var(--ice);
  font-size: 21px;
  line-height: 1.35;
}
.discussion-track {
  height: 5px;
  overflow: hidden;
  border-radius: 999px;
  background: #bad7f71c;
}
.discussion-track > div {
  width: var(--current-value);
  height: 100%;
  border-radius: inherit;
  background: linear-gradient(90deg, var(--chroma-primary), var(--chroma-secondary));
}
.discussion-active .discussion-card {
  animation: discussion-card-in 420ms ease-out var(--card-delay) backwards;
}

@keyframes discussion-card-in {
  from { opacity: 0; transform: translateY(14px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>
