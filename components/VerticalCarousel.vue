<script setup lang="ts">
import { useSlideContext } from '@slidev/client'
import { computed, ref, watch } from 'vue'
import Chat from '~icons/carbon/chat'
import Checklist from '~icons/carbon/list-boxes'
import Completed from '~icons/carbon/task-complete'
import View from '~icons/carbon/view'

const icons = { chat: Chat, checklist: Checklist, completed: Completed, view: View }

const props = defineProps<{
  label: string
  items: { title: string, text: string, icon?: keyof typeof icons }[]
  quote?: boolean
}>()
const { $clicks } = useSlideContext()
const active = computed(() => Math.min(Math.max(0, $clicks.value), props.items.length - 1))
const current = computed(() => props.items[active.value])
const transition = ref('interview-up')

watch(active, (step, previous) => {
  transition.value = step > previous ? 'interview-up' : 'interview-down'
}, { flush: 'sync' })
</script>

<template>
  <div class="interview-carousel" :aria-label="label">
    <div class="interview-viewport">
      <Transition :name="transition">
        <article :key="active" class="glass interview-card">
          <h2>{{ current.title }}</h2>
          <div v-if="current.icon" class="carousel-icon" aria-hidden="true">
            <component :is="icons[current.icon]" />
          </div>
          <blockquote v-if="quote">«{{ current.text }}»</blockquote>
          <p v-else class="carousel-description">{{ current.text }}</p>
        </article>
      </Transition>
    </div>
    <p class="interview-progress" aria-live="polite">{{ active + 1 }} / {{ items.length }}</p>
  </div>
</template>

<style scoped>
.interview-carousel {
  display: grid;
  gap: 14px;
  width: 100%;
}

.interview-viewport {
  position: relative;
  height: 376px;
  overflow: hidden;
}

.interview-carousel .interview-card {
  position: absolute;
  inset: 10px 0;
  width: min(100%, 850px);
  margin-inline: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 24px;
  padding: 30px 46px;
  text-align: center;
}

.interview-card h2 {
  margin: 0;
  color: var(--ice);
  font: 500 29px/1.22 var(--display);
}

.carousel-icon {
  display: grid;
  place-items: center;
  width: 100px;
  height: 100px;
  border: 1px solid var(--line);
  border-radius: 22px;
  background: var(--wash);
  color: var(--chroma-highlight);
  box-shadow: var(--frost-edge);
}

.carousel-icon svg { width: 53px; height: 53px; }

.interview-card .carousel-description {
  max-width: 620px;
  color: var(--muted);
  font-size: 24px;
  line-height: 1.35;
  text-wrap: balance;
}

.interview-card blockquote {
  margin: 0;
  padding: 0 0 0 18px;
  border-left: 2px solid var(--chroma-secondary);
  background: none;
  color: var(--chroma-highlight);
  font: 500 24px/1.35 var(--sans);
}

.interview-progress {
  color: var(--chroma-highlight);
  font-size: 20px;
  text-align: center;
  font-variant-numeric: tabular-nums;
}

@media screen and (prefers-reduced-motion: no-preference) {
  .interview-up-enter-active,
  .interview-up-leave-active,
  .interview-down-enter-active,
  .interview-down-leave-active {
    transition: transform 480ms cubic-bezier(.22,.61,.36,1);
  }

  .interview-up-enter-from,
  .interview-down-leave-to {
    transform: translateY(calc(100% + 20px));
  }

  .interview-up-leave-to,
  .interview-down-enter-from {
    transform: translateY(calc(-100% - 20px));
  }
}
</style>
