<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { computed, watch } from 'vue'

const url = 'https://chromasense.tech/'
const isSlideActive = useIsSlideActive()
const { $clicks, $nav, $renderContext } = useSlideContext()
const inPresentation = computed(() => $renderContext.value === 'slide' || $renderContext.value === 'presenter')
let followingLink = false

watch([isSlideActive, $clicks], ([active, step], [wasActive, previousStep]) => {
  if (!active) {
    followingLink = false
    return
  }
  if (!inPresentation.value || !wasActive || previousStep !== 0 || step !== 1) return

  if (followingLink) {
    followingLink = false
  }
  else if (document.hasFocus()) {
    window.open(url, '_blank', 'noopener,noreferrer')
  }
}, { flush: 'sync' })

function consumeDemoStep() {
  if (!inPresentation.value || !isSlideActive.value || $clicks.value !== 0) return

  followingLink = true
  void $nav.value.next()
}
</script>

<template>
  <a class="live-demo-link" :href="url" target="_blank" rel="noopener noreferrer" @click="consumeDemoStep">ChromaSense</a>
</template>
