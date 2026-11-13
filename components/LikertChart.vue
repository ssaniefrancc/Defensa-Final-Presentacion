<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { useMediaQuery } from '@vueuse/core'
import { computed, ref, watch } from 'vue'

const props = defineProps<{
  counts: [number, number, number, number, number]
}>()

const labels = [
  'Totalmente de acuerdo',
  'De acuerdo',
  'Ni de acuerdo ni en desacuerdo',
  'En desacuerdo',
  'Totalmente en desacuerdo',
]
const axisMax = 35
const ticks = [0, 5, 10, 15, 20, 25, 30, 35]
const isSlideActive = useIsSlideActive()
const { $renderContext } = useSlideContext()
const animateBars = computed(() => isSlideActive.value
  && ($renderContext.value === 'slide' || $renderContext.value === 'presenter'))
const allowMotion = useMediaQuery('screen and (prefers-reduced-motion: no-preference)')
const animateTable = computed(() => animateBars.value && allowMotion.value)
const countDuration = 640
const elapsed = ref<number | null>(null)
const percentFormat = new Intl.NumberFormat('es-PY', { style: 'percent', maximumFractionDigits: 1 })
const total = computed(() => props.counts.reduce((sum, count) => sum + count, 0))
const responses = computed(() => labels.map((label, index) => ({
  label,
  count: props.counts[index],
  ratio: props.counts[index] / total.value,
})))

const rowDelay = (index: number) => 160 + index * 90

watch(animateTable, (active, _, onCleanup) => {
  if (!active) {
    elapsed.value = null
    return
  }

  elapsed.value = 0
  const start = performance.now()
  const duration = rowDelay(labels.length) + countDuration
  let frame = requestAnimationFrame(tick)
  function tick(now: number) {
    const time = now - start
    elapsed.value = time < duration ? time : null
    if (elapsed.value !== null) frame = requestAnimationFrame(tick)
  }
  onCleanup(() => cancelAnimationFrame(frame))
}, { immediate: true })

function rowProgress(index: number) {
  if (elapsed.value === null) return 1
  const progress = Math.min(1, Math.max(0, (elapsed.value - rowDelay(index)) / countDuration))
  return 1 - (1 - progress) ** 3
}

function animatedPercentage(ratio: number, index: number) {
  const progress = rowProgress(index)
  return percentFormat.format(progress === 1 ? ratio : Math.floor(ratio * progress * 100) / 100)
}
</script>

<template>
  <div class="survey-evidence">
    <figure class="glass chart-card" :class="{ 'animate-bars': animateBars }" aria-hidden="true">
      <figcaption>Cantidad de respuestas</figcaption>
      <div class="plot">
        <div v-for="tick in ticks" :key="tick" class="gridline" :style="{ bottom: (tick / axisMax * 100) + '%' }">
          <span>{{ tick }}</span>
        </div>
        <div class="chart-columns">
          <div v-for="(response, index) in responses" :key="response.label" class="chart-column" :style="{ '--bar-delay': rowDelay(index) + 'ms' }">
            <div class="chart-bar" :style="{ height: (response.count / axisMax * 100) + '%' }">
              <span>{{ animatedPercentage(response.ratio, index) }}</span>
            </div>
          </div>
        </div>
      </div>
      <div class="chart-labels">
        <span v-for="response in responses" :key="response.label">{{ response.label }}</span>
      </div>
    </figure>

    <div class="glass table-card" :class="{ 'animate-table': animateTable }">
      <table aria-label="Distribución de las respuestas de la encuesta">
        <thead>
          <tr><th scope="col">Opciones</th><th scope="col">Cantidad</th><th scope="col">Porcentaje</th></tr>
        </thead>
        <tbody>
          <tr v-for="(response, index) in responses" :key="response.label" :style="{ '--row-delay': rowDelay(index) + 'ms' }">
            <th scope="row">{{ response.label }}</th>
            <td><span class="sr-only">{{ response.count }}</span><span class="table-value table-count" aria-hidden="true">{{ Math.floor(response.count * rowProgress(index)) }}</span></td>
            <td><span class="sr-only">{{ percentFormat.format(response.ratio) }}</span><span class="table-value table-percentage" aria-hidden="true">{{ animatedPercentage(response.ratio, index) }}</span></td>
          </tr>
        </tbody>
        <tfoot>
          <tr :style="{ '--row-delay': rowDelay(labels.length) + 'ms' }">
            <th scope="row">TOTAL</th>
            <td><span class="sr-only">{{ total }}</span><span class="table-value table-count" aria-hidden="true">{{ Math.floor(total * rowProgress(labels.length)) }}</span></td>
            <td><span class="sr-only">100%</span><span class="table-value table-percentage" aria-hidden="true">{{ animatedPercentage(1, labels.length) }}</span></td>
          </tr>
        </tfoot>
      </table>
    </div>
  </div>
</template>

<style scoped>
.survey-evidence {
  display: grid;
  grid-template-columns: minmax(0, 1.15fr) minmax(0, 1fr);
  align-items: stretch;
  gap: 20px;
}

.chart-card {
  display: grid;
  grid-template-rows: auto 220px minmax(48px, auto);
  gap: 16px;
  margin: 0;
}

figcaption {
  margin-bottom: 8px;
  color: var(--muted);
  font-size: 16px;
}

.plot {
  position: relative;
  margin-left: 30px;
}

.gridline {
  position: absolute;
  inset-inline: 0;
  border-top: 1px solid color-mix(in srgb, var(--chroma-secondary) 18%, transparent);
}

.gridline span {
  position: absolute;
  right: calc(100% + 9px);
  top: 0;
  transform: translateY(-50%);
  color: var(--muted);
  font-size: 13px;
  font-variant-numeric: tabular-nums;
}

.chart-columns, .chart-labels {
  display: grid;
  grid-template-columns: repeat(5, minmax(0, 1fr));
  gap: 6px;
}

.chart-columns {
  position: absolute;
  inset: 0;
}

.chart-column {
  display: flex;
  align-items: end;
  justify-content: center;
}

.chart-bar {
  position: relative;
  width: 46%;
  border-radius: 6px 6px 0 0;
  background: linear-gradient(0deg, var(--chroma-primary), var(--chroma-secondary));
}

.chart-bar span {
  position: absolute;
  bottom: calc(100% + 6px);
  left: 50%;
  transform: translateX(-50%);
  color: var(--ice);
  font-size: 15px;
  font-weight: 600;
  white-space: nowrap;
}

@media screen and (prefers-reduced-motion: no-preference) {
  .animate-bars .chart-bar {
    animation: grow-bar 640ms cubic-bezier(.22,.61,.36,1) var(--bar-delay) backwards;
  }

  .animate-bars .chart-bar span {
    animation: reveal-value 240ms ease-out var(--bar-delay) backwards;
  }

  .animate-table :is(tbody, tfoot) tr {
    animation: reveal-value 340ms ease-out var(--row-delay) backwards;
  }

  .animate-table .table-value {
    display: inline-block;
    animation: rise-value 480ms ease-out var(--row-delay) backwards;
  }
}

@keyframes grow-bar {
  from { height: 0; }
}

@keyframes reveal-value {
  from { opacity: 0; }
}

@keyframes rise-value {
  from { transform: translateY(8px); }
}

.chart-labels {
  margin-left: 30px;
  color: var(--muted);
  font-size: 13px;
  line-height: 1.3;
  text-align: center;
  text-wrap: balance;
}

.table-card {
  display: grid;
  align-items: center;
}

.table-card table {
  font-size: 16px;
}

.table-card th, .table-card td {
  padding-block: 13px;
}

.table-card tbody th {
  color: var(--muted);
  font-weight: 400;
}

.table-card tbody tr:last-child td {
  border-bottom: 1px solid var(--line);
}

.table-card tfoot th, .table-card tfoot td {
  border-bottom: 0;
  color: var(--ice);
  font-weight: 600;
}
</style>
