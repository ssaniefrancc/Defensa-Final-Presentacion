<script setup lang="ts">
import TypingText from './TypingText.vue'

defineProps<{ text: string, plain?: boolean, delay?: number, interval?: number, fadeOnly?: boolean }>()
</script>

<template>
  <div :class="{ 'glass statement typing-statement': !plain }">
    <p><TypingText :text="text" :delay="delay" :interval="interval" :fade-only="fadeOnly" /></p>
  </div>
</template>

<style scoped>
.typing-statement {
  align-self: center;
  text-align: center;
}
</style>
