<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { computed, useId } from 'vue'

const isSlideActive = useIsSlideActive()
const { $renderContext } = useSlideContext()
const animate = computed(() => isSlideActive.value
  && ($renderContext.value === 'slide' || $renderContext.value === 'presenter'))
const arrowId = useId() + '-module-arrow'
const actors = [
  { name: 'Administrador', position: 'system-admin' },
  { name: 'Clientes', position: 'system-clients' },
]
const modules = [
  { label: 'Módulo de dashboard y analítica', y: 112, clients: false },
  { label: 'Módulo de inicio y encuesta previa', y: 205, clients: true },
  { label: 'Módulo de análisis de colorimetría', y: 298, clients: true },
  { label: 'Módulo de encuestas y feedback', y: 391, clients: true },
]
</script>

<template>
  <figure class="system-diagram" :class="{ 'system-diagram-active': animate }" aria-label="Actores y módulos de ChromaSense">
    <section class="system-boundary" aria-label="Sistema ChromaSense">
      <h2>Sistema ChromaSense</h2>
    </section>

    <svg class="system-links" viewBox="0 0 1080 450" :style="{ '--arrow-marker': 'url(#' + arrowId + ')' }" aria-hidden="true">
      <defs>
        <marker :id="arrowId" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto">
          <path d="M0 0 L10 5 L0 10 Z" />
        </marker>
      </defs>
      <g v-for="(module, index) in modules" :key="module.label" :style="{ '--arrow-delay': (210 + index * 155) + 'ms' }">
        <line class="admin-link" x1="200" y1="156" x2="303" :y2="module.y" />
        <line v-if="module.clients" class="client-link" x1="880" y1="298" x2="777" :y2="module.y" />
      </g>
    </svg>

    <div v-for="actor in actors" :key="actor.name" class="glass system-actor" :class="actor.position">
      <svg class="actor-icon" viewBox="0 0 48 64" aria-hidden="true">
        <circle cx="24" cy="12" r="8" />
        <path d="M24 20v22m-17-15h34M24 42 11 60m13-18 13 18" />
      </svg>
      {{ actor.name }}
    </div>
    <div v-for="module in modules" :key="module.label" class="glass system-module" :style="{ top: (module.y - 31) + 'px' }">
      {{ module.label }}
      <span class="sr-only">. Acceso: {{ module.clients ? 'administrador y clientes' : 'administrador' }}.</span>
    </div>
  </figure>
</template>

<style scoped>
.system-diagram {
  position: relative;
  width: 1080px;
  height: 450px;
  margin: 0 auto;
}

.system-boundary {
  position: absolute;
  inset: 0 268px;
  border: 1px solid var(--line);
  border-radius: 18px;
  background: var(--wash);
}

.system-boundary h2 {
  margin: 0;
  padding: 17px 20px;
  border-bottom: 1px solid var(--line);
  color: var(--chroma-highlight);
  font: 500 22px/1.2 var(--display);
  text-align: center;
}

.system-links {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}

.system-links line {
  stroke: var(--chroma-secondary);
  stroke-width: 1.7;
  opacity: .75;
  marker-end: var(--arrow-marker);
  transform-box: view-box;
}

.system-links marker path { fill: var(--chroma-secondary); }
.system-links .admin-link { transform-origin: 200px 156px; }
.system-links .client-link { transform-origin: 880px 298px; }

@media screen and (prefers-reduced-motion: no-preference) {
  .system-diagram-active .system-links line {
    animation: connect-module 540ms cubic-bezier(.22,.61,.36,1) var(--arrow-delay) backwards;
  }
}

@keyframes connect-module {
  from { transform: scale(0); opacity: 0; }
}

.system-diagram .system-actor,
.system-diagram .system-module {
  position: absolute;
  display: grid;
  place-items: center;
  padding: 0 16px;
  color: var(--ice);
  text-align: center;
}

.system-diagram .system-actor {
  width: 190px;
  height: 62px;
  font: 500 23px/1.2 var(--display);
}

.system-admin { left: 10px; top: 125px; }
.system-clients { right: 10px; top: 267px; }

.actor-icon {
  position: absolute;
  bottom: calc(100% + 12px);
  left: 50%;
  width: 46px;
  height: 61px;
  transform: translateX(-50%);
  fill: none;
  stroke: var(--chroma-highlight);
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.system-diagram .system-module {
  left: 305px;
  width: 470px;
  height: 62px;
  border-radius: 999px;
  font: 500 20px/1.25 var(--sans);
}
</style>
