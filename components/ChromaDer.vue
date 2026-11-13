<script setup lang="ts">
import { useIsSlideActive, useSlideContext } from '@slidev/client'
import { computed } from 'vue'

const isSlideActive = useIsSlideActive()
const { $renderContext } = useSlideContext()
const animate = computed(() => isSlideActive.value
  && ($renderContext.value === 'slide' || $renderContext.value === 'presenter'))

type Field = [type: string, name: string, key?: string]
type Entity = { name: string, x: number, y: number, width: number, fields: Field[] }

const entities: Entity[] = [
  { name: 'IMAGES', x: 0, y: 0, width: 242, fields: [
    ['bigint', 'id', 'PK'], ['varchar', 'filepath'], ['varchar', 'filename'],
    ['varchar', 'sha256', 'UK'], ['integer', 'legacy_web_id', 'UK'], ['integer', 'legacy_reference_id', 'UK'],
  ] },
  { name: 'IMAGE_REFERENCES', x: 292, y: 0, width: 242, fields: [
    ['bigint', 'id', 'PK'], ['bigint', 'image_id', 'FK, UK'], ['integer', 'legacy_reference_id', 'UK'],
    ['varchar', 'confirmed_season'], ['varchar', 'label_status'], ['timestamp', 'created_at'],
  ] },
  { name: 'USERS', x: 894, y: 0, width: 210, fields: [
    ['bigint', 'id', 'PK'], ['varchar', 'participant_code', 'UK'], ['varchar', 'display_name'],
  ] },
  { name: 'REFERENCE_SIMULATED_RATINGS', x: 292, y: 199, width: 242, fields: [
    ['bigint', 'reference_id', 'PK, FK'], ['integer', 'rating'], ['timestamp', 'created_at'],
  ] },
  { name: 'ANALYSIS_SESSIONS', x: 580, y: 109, width: 265, fields: [
    ['bigint', 'id', 'PK'], ['bigint', 'user_id', 'FK'], ['bigint', 'reference_id', 'FK, UK'],
    ['bigint', 'web_id', 'UK'], ['text', 'source'], ['varchar', 'declared_name'], ['timestamp', 'created_at'],
    ['integer', 'legacy_web_id', 'UK'], ['integer', 'legacy_reference_id', 'UK'],
    ['integer', 'legacy_participant_id', 'UK'], ['timestamp', 'participant_registered_at'],
  ] },
  { name: 'COLOR_ANALYSES', x: 0, y: 225, width: 242, fields: [
    ['bigint', 'id', 'PK'], ['bigint', 'session_id', 'FK'], ['bigint', 'image_id', 'FK'],
    ['varchar', 'predicted_season'], ['json', 'detected_colors'], ['json', 'chromatic_profile'],
    ['json', 'seasonal_palette'], ['text', 'recommendations'], ['json', 'legacy_palette'],
    ['boolean', 'legacy_snapshot'], ['timestamp', 'analyzed_at'],
  ] },
  { name: 'SURVEY_RESPONSES', x: 894, y: 290, width: 210, fields: [
    ['bigint', 'session_id', 'PK, FK'], ['text', 'kind', 'PK'], ['json', 'answers'],
    ['integer', 'rating'], ['boolean', 'rating_is_demo'], ['text', 'comments'], ['timestamp', 'submitted_at'],
  ] },
]

const links = [
  { line: 'M180 136 V158 H345 V136', label: 'puede ser referencia', x: 262, y: 177, ends: [[161, 150, '1'], [363, 150, '0..1']] },
  { line: 'M115 136 V225', label: 'es la imagen analizada', x: 185, y: 187, ends: [[96, 150, '0..1'], [96, 218, '0..N']] },
  { line: 'M435 136 V199', label: 'puede tener', x: 481, y: 168, ends: [[449, 150, '1'], [455, 192, '0..1']] },
  { line: 'M534 91 H557 V151 H580', label: 'origina una sesión', x: 603, y: 83, ends: [[553, 107, '0..1'], [559, 144, '0..1']] },
  { line: 'M894 49 H873 V145 H845', label: 'identifica a la persona', x: 975, y: 118, ends: [[876, 40, '0..1'], [870, 163, '0..N']] },
  { line: 'M242 316 H546 V304 H580', label: 'contiene', x: 411, y: 306, ends: [[269, 306, '0..N'], [565, 296, '1']] },
  { line: 'M845 320 H894', label: 'recibe', x: 870, y: 348, ends: [[856, 311, '1'], [878, 337, '0..N']] },
]
</script>

<template>
  <figure class="document-der" :class="{ 'der-animating': animate }" aria-label="DER de la figura 86 de la tesis">
    <svg class="document-der-links" viewBox="0 0 1104 452" aria-label="Siete relaciones y sus cardinalidades">
      <g v-for="(link, index) in links" :key="link.label" :style="{ '--link-delay': (210 + index * 155) + 'ms' }">
        <path :d="link.line" pathLength="1" />
        <text class="relation-name" :x="link.x" :y="link.y">{{ link.label }}</text>
        <text v-for="[x, y, value] in link.ends" :key="x + ',' + y" :x="x" :y="y">{{ value }}</text>
      </g>
    </svg>

    <section v-for="entity in entities" :key="entity.name" class="der-table" :style="{ left: entity.x + 'px', top: entity.y + 'px', width: entity.width + 'px' }">
      <h2>{{ entity.name }}</h2>
      <table :aria-label="entity.name">
        <colgroup><col class="der-type"><col><col class="der-key"></colgroup>
        <tbody>
          <tr v-for="[type, name, key] in entity.fields" :key="name">
            <td>{{ type }}</td><th scope="row">{{ name }}</th><td>{{ key }}</td>
          </tr>
        </tbody>
      </table>
    </section>

    <figcaption>
      <span>PK primaria · FK foránea · UK única</span>
      <a href="/evidencia/entidad-relacion.png" target="_blank" rel="noopener">Ver figura original ↗</a>
    </figcaption>
  </figure>
</template>

<style scoped>
.document-der {
  position: relative;
  width: 1104px;
  height: 477px;
  margin: 0 auto;
}
.document-der-links {
  position: absolute;
  inset: 0;
  width: 1104px;
  height: 452px;
}
.document-der-links path {
  fill: none;
  stroke: var(--chroma-secondary);
  stroke-width: 1.3;
  opacity: .75;
}
.document-der-links text {
  fill: var(--chroma-highlight);
  font: 500 11px var(--sans);
  text-anchor: middle;
  paint-order: stroke;
  stroke: #100d23;
  stroke-width: 3px;
}
.document-der-links .relation-name { fill: var(--muted); }

@media screen and (prefers-reduced-motion: no-preference) {
  .der-animating .document-der-links path {
    stroke-dasharray: 1 1;
    animation: draw-der-link 540ms cubic-bezier(.22,.61,.36,1) var(--link-delay) backwards;
  }

  .der-animating .document-der-links text {
    animation: show-der-label 240ms ease-out calc(var(--link-delay) + 540ms) backwards;
  }
}

@keyframes draw-der-link {
  from { stroke-dashoffset: 1; }
  to { stroke-dashoffset: 0; }
}

@keyframes show-der-label {
  from { opacity: 0; }
}

.der-table {
  position: absolute;
  overflow: hidden;
  border: 1px solid var(--line);
  border-radius: 10px;
  background: #111326;
  box-shadow: var(--frost-edge);
}
.der-table h2 {
  display: grid;
  height: 26px;
  place-items: center;
  margin: 0;
  background: color-mix(in srgb, var(--chroma-primary) 16%, #1b2039);
  color: var(--ice);
  font: 600 12px/1 var(--sans);
  letter-spacing: .025em;
}
.der-table table {
  table-layout: fixed;
  width: 100%;
  margin: 0;
  border-collapse: collapse;
  font: 400 11.5px/1 ui-monospace, Consolas, monospace;
}
.der-type { width: 64px; }
.der-key { width: 45px; }
.der-table table[aria-label="USERS"] .der-type { width: 52px; }
.der-table table[aria-label="USERS"] .der-key { width: 33px; }
.der-table :is(th, td) {
  height: 18px;
  padding: 0 5px;
  border: 0;
  border-top: 1px solid #bad7f71c;
  color: var(--muted);
  text-align: left;
  white-space: nowrap;
}
.der-table th { color: var(--ice); font-weight: 500; }
.der-table td:last-child { color: var(--chroma-highlight); }
.der-table tr:nth-child(even) { background: #bad7f70a; }

.document-der figcaption {
  position: absolute;
  bottom: 0;
  inset-inline: 0;
  display: flex;
  justify-content: space-between;
  color: var(--muted);
  font-size: 13px;
}
.document-der a { color: var(--chroma-highlight); }
</style>
