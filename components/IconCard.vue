<script setup lang="ts">
import Store        from '~icons/carbon/store'
import Cloud        from '~icons/carbon/cloud-services'
import People       from '~icons/carbon/user-multiple'
import WifiOff      from '~icons/carbon/wifi-off'

const icons = {
  store:   Store,
  cloud:   Cloud,
  people:  People,
  wifioff: WifiOff,
}

defineProps<{
  icon: keyof typeof icons
  title: string
}>()
</script>

<template>
  <div class="icon-card-header">
    <div class="icon-card-badge" aria-hidden="true">
      <component :is="icons[icon]" />
    </div>
    <h3>{{ title }}</h3>
  </div>
  <slot />
</template>

<style scoped>
.icon-card-header {
  display: flex;
  align-items: center;
  gap: 14px;
  margin-bottom: 12px;
}
.icon-card-header h3 {
  margin: 0;
  font-size: 20px;
  font-weight: 500;
  color: var(--ice);
  line-height: 1.2;
}
.icon-card-badge {
  display: grid;
  place-items: center;
  width: 42px;
  height: 42px;
  flex-shrink: 0;
  border: 1px solid var(--line);
  border-radius: 10px;
  background: var(--wash);
  color: var(--chroma-secondary);
  box-shadow: var(--frost-edge);
}
.icon-card-badge svg {
  width: 22px;
  height: 22px;
}
</style>
