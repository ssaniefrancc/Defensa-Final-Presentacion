<script setup lang="ts">
/**
 * CardText — renders text with the same entrance typing animation used in
 * AnimatedTextCards / slide 38 (Conclusiones).
 *
 * Props:
 *   text       – the string to animate
 *   cardOrder  – matches the --card-order on the parent .glass card (0-based).
 *                Used to stagger the typing start after the card fade-in.
 *   extraDelay – additional ms to wait on top of the card-entrance delay.
 *                Use when multiple CardText live inside the same .glass card.
 *   tag        – rendered HTML element (default: 'p')
 *   interval   – ms between letters (default: 11)
 *   fadeOnly   – use fade-only variant instead of slide-up per letter
 */
import TypingText from './TypingText.vue'

const props = withDefaults(defineProps<{
  text: string
  cardOrder?: number
  extraDelay?: number
  tag?: string
  interval?: number
  fadeOnly?: boolean
}>(), {
  cardOrder: 0,
  extraDelay: 0,
  tag: 'p',
  interval: 11,
  fadeOnly: false,
})

// Card entrance finishes at: 140ms + cardOrder*130ms + 420ms (animation duration)
// Add a small extra gap (60ms) before typing starts, plus any extraDelay.
const typingDelay = 140 + props.cardOrder * 130 + 420 + 60 + props.extraDelay
</script>

<template>
  <component :is="tag">
    <TypingText :text="text" :delay="typingDelay" :interval="interval" :fade-only="fadeOnly" />
  </component>
</template>
