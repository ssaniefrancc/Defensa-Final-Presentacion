---
theme: default
title: ChromaSense · Defensa de tesis
aspectRatio: 16/9
canvasWidth: 1280
colorSchema: dark
transition: slide-up
fonts:
  provider: none
layout: none
class: thesis-slide hero-slide
clicks: 1
---

<CoverReveal>
<div class="hero">
  <p class="eyebrow cover-copy" style="--copy-delay: 0ms">Trabajo final de grado · Ingeniería Informática</p>
  <p class="wordmark">ChromaSense</p>
  <h1 class="cover-copy" style="--copy-delay: 80ms">DESARROLLO DE UN SISTEMA DE RECOMENDACIÓN DE VESTIMENTAS Y COLORIMETRÍA MEDIANTE MACHINE LEARNING PARA LADY DI MODAS CAACUPÉ, AÑO 2026</h1>
  <p class="cover-date cover-copy" style="--copy-delay: 160ms">Universidad del Norte · Caacupé, noviembre de 2026</p>
  <div class="cover-spectrum" aria-hidden="true"><i></i><i></i><i></i><i></i><i></i><i></i></div>
</div>
<div class="cover-university">
  <img src="/evidencia/logos/uninorte.png" alt="Escudo de la Universidad del Norte">
</div>
</CoverReveal>

<!--
Pulsar Siguiente para activar la portada a color. Presentar el trabajo final de graduación y el contexto de Lady Di Modas, Caacupé.
-->

---
layout: none
class: thesis-slide 
title: 'AUTORES Y TUTOR'
transition: slide-left
---

<main class="frame">
<h1 class="slide-title">AUTORES Y TUTOR</h1>
<DefenseCredits tutor="Mgtr. Fernando Romero" :authors='[
  { "given": "Derlis Gustavo", "family": "Centurión Estigarribia" },
  { "given": "Santiago Daniel", "family": "Franco Cañete" }
]' />
</main>

---
layout: none
class: thesis-slide 
title: 'INTRODUCCIÓN'
transition: slide-down
---

<SlideFrame>
<h1 class="slide-title">INTRODUCCIÓN</h1>
<p class="lead">ChromaSense recomienda colores y prendas a partir de las características cromáticas de cada clienta.</p>
<div class="gridcards">
  <div class="glass" style="--card-order:0"><h3>Contexto</h3><CardText text="Asesoría de imagen en Lady Di Modas, Caacupé." :card-order="0" /></div>
  <div class="glass" style="--card-order:1"><h3>Solución</h3><CardText text="Plataforma web con visión por computadora y Machine Learning." :card-order="1" /></div>
</div>
</SlideFrame>

<!--
La evaluación combinó una entrevista con la propietaria y encuestas a las clientas antes y después del uso del sistema. Tesis, introducción.
-->

---
layout: none
class: thesis-slide chapter-slide
title: 'PLANTEAMIENTO DEL PROBLEMA'
transition: slide-right
---

<main class="frame">
<ChapterHeading label="CAPÍTULO I" title="PLANTEAMIENTO DEL PROBLEMA" />
</main>

---
layout: none
class: thesis-slide 
title: 'PLANTEAMIENTO'
transition: slide-up
---

<SlideFrame>
<h1 class="slide-title">PLANTEAMIENTO</h1>
<p class="lead">La indecisión al elegir vestimentas</p>
<div class="gridcards">
  <div class="glass" style="--card-order:0"><h3>Inseguridad</h3><CardText text="Dudas sobre los colores que favorecen los rasgos personales." :card-order="0" /></div>
  <div class="glass" style="--card-order:1"><h3>Dependencia</h3><CardText text="La elección suele apoyarse en el criterio del personal de ventas." :card-order="1" /></div>
  <div class="glass" style="--card-order:2"><h3>Tiempo</h3><CardText text="Las dudas pueden prolongar el proceso de compra." :card-order="2" /></div>
</div>
</SlideFrame>

---
layout: none
class: thesis-slide 
title: 'PREGUNTA PRINCIPAL'
transition: slide-left
---

<SlideFrame>
<h1 class="slide-title">PREGUNTA PRINCIPAL</h1>
<div class="glass statement" style="--card-order:0">
  <CardText text="¿En qué medida un sistema de recomendación de vestimentas y colorimetría basado en Machine Learning (Chroma Sense) contribuye a reducir el tiempo de indecisión de las clientas de Lady Di Modas al seleccionar prendas, en la ciudad de Caacupé, durante el año 2026?" :card-order="0" />
</div>
</SlideFrame>

---
layout: none
class: thesis-slide 
title: 'PREGUNTAS ESPECÍFICAS'
transition: slide-down
clicks: 3
---

<main class="frame">
<h1 class="slide-title">PREGUNTAS ESPECÍFICAS</h1>
<QuestionCarousel label="Preguntas específicas" :items='[
  "¿Qué dificultades y vivencias manifiestan las clientas de Lady Di Modas al seleccionar vestimentas acordes a sus características cromáticas, en la ciudad de Caacupé, durante el año 2026?",
  "¿Cómo se desarrolla actualmente el proceso de selección de prendas y qué factores inciden en el tiempo que las clientas de Lady Di Modas dedican a decidir, en la ciudad de Caacupé, durante el año 2026?",
  "¿Cómo puede un sistema basado en Machine Learning generar recomendaciones personalizadas de vestimentas y colores a partir de las características cromáticas de las clientas de Lady Di Modas, en la ciudad de Caacupé, durante el año 2026?",
  "¿De qué manera el conocimiento de las características cromáticas personales influye en los criterios de selección de vestimentas de las clientas de Lady Di Modas, en la ciudad de Caacupé, durante el año 2026?"
]' />
</main>

---
layout: none
class: thesis-slide 
title: 'OBJETIVO GENERAL'
transition: slide-right
---

<SlideFrame>
<h1 class="slide-title">OBJETIVO GENERAL</h1>
<div class="glass statement" style="--card-order:0">
  <CardText text="Determinar la contribución de un sistema de recomendación de vestimentas y colorimetría basado en Machine Learning (Chroma Sense) a la reducción del tiempo de indecisión de las clientas de Lady Di Modas al seleccionar prendas, en la ciudad de Caacupé, durante el año 2026." :card-order="0" />
</div>
</SlideFrame>

---
layout: none
class: thesis-slide 
title: 'OBJETIVOS ESPECÍFICOS'
transition: slide-up
clicks: 3
---

<main class="frame">
<h1 class="slide-title">OBJETIVOS ESPECÍFICOS</h1>
<QuestionCarousel label="Objetivos específicos" :items='[
  "Identificar las dificultades y vivencias de las clientas de Lady Di Modas al seleccionar vestimentas acordes a sus características cromáticas, en la ciudad de Caacupé, durante el año 2026.",
  "Describir el proceso actual de selección de prendas y los factores que inciden en el tiempo que las clientas de Lady Di Modas dedican a decidir, en la ciudad de Caacupé, durante el año 2026.",
  "Desarrollar un sistema basado en Machine Learning que genere recomendaciones personalizadas de vestimentas y colores a partir de las características cromáticas de las clientas de Lady Di Modas, en la ciudad de Caacupé, durante el año 2026.",
  "Analizar la influencia del conocimiento de las características cromáticas personales en los criterios de selección de vestimentas de las clientas de Lady Di Modas, en la ciudad de Caacupé, durante el año 2026."
]' />
</main>

---
layout: none
class: thesis-slide 
title: 'JUSTIFICACIÓN'
transition: slide-left
---

<SlideFrame>
<h1 class="slide-title">JUSTIFICACIÓN</h1>
<div class="glass rationale-panel" style="--card-order:0">
  <CardText class="rationale-main" text="Las dudas sobre qué colores favorecen a cada clienta pueden alargar la decisión de compra." :card-order="0" tag="p" />
  <CardText text="ChromaSense aporta un criterio cromático para orientar esa elección." :card-order="0" :extra-delay="1100" tag="p" />
</div>
</SlideFrame>

---
layout: none
class: thesis-slide 
title: 'DELIMITACIÓN'
transition: slide-down
---

<SlideFrame>
<h1 class="slide-title">DELIMITACIÓN</h1>
<dl class="glass scope-sheet" style="--card-order:0">
  <div><dt>Lugar</dt><CardText text="Lady Di Modas, Caacupé." :card-order="0" tag="dd" /></div>
  <div><dt>Periodo</dt><CardText text="Desarrollo y evaluación durante 2026." :card-order="0" :extra-delay="260" tag="dd" /></div>
  <div><dt>Alcance</dt><CardText text="Recomendación de prendas y colores." :card-order="0" :extra-delay="520" tag="dd" /></div>
</dl>
</SlideFrame>

---
layout: none
class: thesis-slide 
title: 'IMPACTO'
transition: slide-right
---

<SlideFrame>
<h1 class="slide-title">IMPACTO</h1>
<div class="impact-overview">
  <p class="impact-label">Impacto esperado</p>
  <div class="impact-beneficiaries">
    <section class="glass" style="--card-order:0">
      <h2>Clientas</h2>
      <CardText text="Mayor seguridad al elegir colores y prendas." :card-order="0" />
    </section>
    <section class="glass" style="--card-order:1">
      <h2>Lady Di Modas</h2>
      <CardText text="Apoyo a la asesoría de imagen en tienda." :card-order="1" />
    </section>
  </div>
</div>
</SlideFrame>

<!--
Estos son los beneficios esperados al formular el proyecto. Los resultados de la evaluación se presentan en el capítulo IV.
-->

---
layout: none
class: thesis-slide chapter-slide
title: 'MARCO TEÓRICO'
transition: slide-up
---

<main class="frame">
<ChapterHeading label="CAPÍTULO II" title="MARCO TEÓRICO" />
</main>

---
layout: none
class: thesis-slide tools-slide
title: 'HERRAMIENTAS / TECNOLOGÍAS'
transition: slide-left
clicks: 8
---

<main class="frame">
  <h1 class="slide-title">HERRAMIENTAS / TECNOLOGÍAS</h1>
  <p class="tools-category">Interfaz, servidor y base de datos</p>
  <ToolWave>
    <div class="glass tool-card" style="--wave-order: 0">
      <img class="tool-logo" src="/evidencia/logos/react.png" alt="">
      <h3>React</h3><p>Interfaz de usuario</p>
    </div>
    <div class="glass tool-card" style="--wave-order: 1">
      <img class="tool-logo" src="/evidencia/logos/vite.png" alt="">
      <h3>Vite</h3><p>Desarrollo y compilación web</p>
    </div>
    <div class="glass tool-card" style="--wave-order: 2">
      <img class="tool-logo" src="/evidencia/logos/python.png" alt="">
      <h3>Python</h3><p>Lógica del servidor</p>
    </div>
    <div class="glass tool-card" style="--wave-order: 3">
      <img class="tool-logo tool-logo-light" src="/evidencia/logos/flask.png" alt="">
      <h3>Flask</h3><p>Servicios del backend</p>
    </div>
    <div class="glass tool-card" style="--wave-order: 4">
      <img class="tool-logo tool-logo-light" src="/evidencia/logos/rest.png" alt="">
      <h3>API REST</h3><p>Comunicación entre interfaz y servidor</p>
    </div>
    <div class="glass tool-card" style="--wave-order: 5">
      <img class="tool-logo" src="/evidencia/logos/postgresql.png" alt="">
      <h3>PostgreSQL</h3><p>Almacenamiento relacional</p>
    </div>
    <div class="glass tool-card" style="--wave-order: 6">
      <img class="tool-logo tool-logo-light" src="/evidencia/logos/sqlalchemy.png" alt="">
      <h3>SQLAlchemy</h3><p>Mapeo entre modelos y base de datos</p>
    </div>
    <div class="glass tool-card" style="--wave-order: 7">
      <img class="tool-logo tool-logo-light" src="/evidencia/logos/flask-sqlalchemy.png" alt="">
      <h3>Flask-SQLAlchemy</h3><p>Integración de modelos con Flask</p>
    </div>
  </ToolWave>
</main>

---
layout: none
class: thesis-slide tools-slide
title: 'HERRAMIENTAS / TECNOLOGÍAS'
transition: slide-down
clicks: 8
---

<main class="frame">
  <h1 class="slide-title">HERRAMIENTAS / TECNOLOGÍAS</h1>
  <p class="tools-category">Visión, análisis cromático e inteligencia artificial</p>
  <ToolWave>
    <div class="glass tool-card" style="--wave-order: 0">
      <img class="tool-logo tool-logo-light" src="/evidencia/logos/opencv.png" alt="">
      <h3>OpenCV</h3><p>Procesamiento de imágenes</p>
    </div>
    <div class="glass tool-card" style="--wave-order: 1">
      <img class="tool-logo" src="/evidencia/logos/mediapipe.png" alt="">
      <h3>MediaPipe</h3><p>Detección de puntos faciales</p>
    </div>
    <div class="glass tool-card" style="--wave-order: 2">
      <img class="tool-logo tool-logo-light" src="/evidencia/logos/numpy.png" alt="">
      <h3>NumPy</h3><p>Operaciones sobre píxeles y matrices</p>
    </div>
    <div class="glass tool-card" style="--wave-order: 3">
      <img class="tool-logo tool-logo-light" src="/evidencia/logos/github.png" alt="">
      <h3>SkinToneClassifier</h3><p>Estimación del tono de piel</p>
    </div>
    <div class="glass tool-card" style="--wave-order: 4">
      <img class="tool-logo tool-logo-light" src="/evidencia/logos/paleta-perla.jpg" alt="">
      <h3>Paleta Perla</h3><p>Referencia cromática para tonos de piel</p>
    </div>
    <div class="glass tool-card" style="--wave-order: 5">
      <img class="tool-logo tool-logo-light" src="/evidencia/logos/gemini.png" alt="">
      <h3>Gemini</h3><p>Generación de recomendaciones</p>
    </div>
    <div class="glass tool-card" style="--wave-order: 6">
      <img class="tool-logo tool-logo-light" src="/evidencia/logos/google-apis.png" alt="">
      <h3>Google Gen AI SDK</h3><p>Integración con Gemini</p>
    </div>
    <div class="glass tool-card" style="--wave-order: 7">
      <img class="tool-logo tool-logo-light" src="/evidencia/logos/plotly.svg" alt="">
      <h3>Plotly.js</h3><p>Visualización en el panel de analítica</p>
    </div>
  </ToolWave>
</main>

---
layout: none
class: thesis-slide formula-slide
title: 'FUNDAMENTOS MATEMÁTICOS DEL ANÁLISIS CROMÁTICO'
transition: slide-right
---

<main class="frame">
  <h1 class="slide-title">FUNDAMENTOS MATEMÁTICOS DEL ANÁLISIS CROMÁTICO</h1>
  <p class="formula-subtitle">Coordenadas faciales</p>
  <div class="glass formula-panel">
    <math display="block"><mrow><mrow><mi>x</mi><mo>=</mo><mrow><mo>⌊</mo><mi>u</mi><mi>W</mi><mo>⌋</mo></mrow></mrow><mo>,</mo><mspace width="0.6em"/><mrow><mi>y</mi><mo>=</mo><mrow><mo>⌊</mo><mi>v</mi><mi>H</mi><mo>⌋</mo></mrow></mrow></mrow></math>
  </div>
  <p class="formula-caption">La imagen es una matriz de H × W × 3. MediaPipe entrega u y v normalizados. W y H son el ancho y el alto en píxeles.</p>
</main>

---
layout: none
class: thesis-slide formula-slide
title: 'ESTIMACIÓN DEL COLOR REPRESENTATIVO'
transition: slide-up
clicks: 1
---

<main class="frame">
  <h1 class="slide-title">ESTIMACIÓN DEL COLOR REPRESENTATIVO</h1>
  <p class="formula-subtitle">Percentiles y mediana</p>
  <QuestionCarousel class="formula-carousel" label="Percentiles y mediana" :items="['Fórmula 1', 'Fórmula 2']">
    <template #item-0>
      <math display="block"><mrow><msub><mi>P</mi><mn>10</mn></msub><mo>≤</mo><msub><mi>g</mi><mi>i</mi></msub><mo>≤</mo><msub><mi>P</mi><mn>90</mn></msub></mrow></math>
    </template>
    <template #item-1>
      <math class="formula-long" display="block"><mrow><mi>ĉ</mi><mo>=</mo><mrow><mo>(</mo><mrow><mi mathvariant="normal">med</mi><mrow><mo>(</mo><mi>B</mi><mo>)</mo></mrow></mrow><mo>,</mo><mrow><mi mathvariant="normal">med</mi><mrow><mo>(</mo><mi>G</mi><mo>)</mo></mrow></mrow><mo>,</mo><mrow><mi mathvariant="normal">med</mi><mrow><mo>(</mo><mi>R</mi><mo>)</mo></mrow></mrow><mo>)</mo></mrow></mrow></math>
    </template>
  </QuestionCarousel>
  <p class="formula-caption">El filtro conserva las intensidades entre los percentiles 10 y 90. La mediana de cada canal BGR se calcula sobre esos píxeles.</p>
</main>

---
layout: none
class: thesis-slide formula-slide
title: 'CROMA Y MATIZ EN CIELAB'
transition: slide-left
clicks: 1
---

<main class="frame">
  <h1 class="slide-title">CROMA Y MATIZ EN CIELAB</h1>
  <QuestionCarousel class="formula-carousel" label="CROMA Y MATIZ EN CIELAB" :items="['Fórmula 1', 'Fórmula 2']">
    <template #item-0>
      <math display="block"><mrow><msup><mi>C</mi><mo>∗</mo></msup><mo>=</mo><msqrt><mrow><msup><mrow><mo>(</mo><msup><mi>a</mi><mo>∗</mo></msup><mo>)</mo></mrow><mn>2</mn></msup><mo>+</mo><msup><mrow><mo>(</mo><msup><mi>b</mi><mo>∗</mo></msup><mo>)</mo></mrow><mn>2</mn></msup></mrow></msqrt></mrow></math>
    </template>
    <template #item-1>
      <math display="block"><mrow><mi>h</mi><mo>=</mo><mrow><mrow><mi mathvariant="normal">atan2</mi><mrow><mo>(</mo><msup><mi>b</mi><mo>∗</mo></msup><mo>,</mo><msup><mi>a</mi><mo>∗</mo></msup><mo>)</mo></mrow></mrow><mo>×</mo><mfrac><mn>180</mn><mi>π</mi></mfrac></mrow></mrow></math>
    </template>
  </QuestionCarousel>
  <p class="formula-caption">El croma mide la intensidad del color. El ángulo de matiz se expresa en grados.</p>
</main>

---
layout: none
class: thesis-slide formula-slide
title: 'INDICADORES CROMÁTICOS'
transition: slide-down
clicks: 1
---

<main class="frame">
  <h1 class="slide-title">INDICADORES CROMÁTICOS</h1>
  <p class="formula-subtitle">Calidez y claridad</p>
  <QuestionCarousel class="formula-carousel" label="Calidez y claridad" :items="['Fórmula 1', 'Fórmula 2']">
    <template #item-0>
      <math display="block"><mrow><mi>T</mi><mo>=</mo><mrow><mi mathvariant="normal">limitar</mi><mrow><mo>(</mo><mfrac><mrow><msub><mi>h</mi><mtext>piel</mtext></msub><mo>−</mo><mn>52</mn></mrow><mn>15</mn></mfrac><mo>,</mo><mn>−1</mn><mo>,</mo><mn>1</mn><mo>)</mo></mrow></mrow></mrow></math>
    </template>
    <template #item-1>
      <math display="block"><mrow><msub><mi>L</mi><mi>g</mi></msub><mo>=</mo><mrow><mn>0,65</mn><msub><msup><mi>L</mi><mo>∗</mo></msup><mtext>piel</mtext></msub><mo>+</mo><mn>0,35</mn><msub><msup><mi>L</mi><mo>∗</mo></msup><mtext>cabello</mtext></msub></mrow></mrow></math>
    </template>
  </QuestionCarousel>
  <p class="formula-caption">La calidez parte del matiz de la piel. La claridad combina la piel y el cabello.</p>
</main>

---
layout: none
class: thesis-slide formula-slide
title: 'INDICADORES CROMÁTICOS'
transition: slide-right
clicks: 1
---

<main class="frame">
  <h1 class="slide-title">INDICADORES CROMÁTICOS</h1>
  <p class="formula-subtitle">Contraste y croma general</p>
  <QuestionCarousel class="formula-carousel" label="Contraste y croma general" :items="['Fórmula 1', 'Fórmula 2']">
    <template #item-0>
      <math display="block"><mrow><msub><mi>D</mi><mi>L</mi></msub><mo>=</mo><mrow><mo>|</mo><msub><msup><mi>L</mi><mo>∗</mo></msup><mtext>piel</mtext></msub><mo>−</mo><msub><msup><mi>L</mi><mo>∗</mo></msup><mtext>cabello</mtext></msub><mo>|</mo></mrow></mrow></math>
    </template>
    <template #item-1>
      <math class="formula-long" display="block"><mrow><msub><mi>C</mi><mi>g</mi></msub><mo>=</mo><mrow><mn>0,55</mn><msub><msup><mi>C</mi><mo>∗</mo></msup><mtext>piel</mtext></msub><mo>+</mo><mn>0,25</mn><msub><msup><mi>C</mi><mo>∗</mo></msup><mtext>cabello</mtext></msub><mo>+</mo><mn>0,20</mn><msub><msup><mi>C</mi><mo>∗</mo></msup><mtext>iris</mtext></msub></mrow></mrow></math>
    </template>
  </QuestionCarousel>
  <p class="formula-caption">El contraste es la diferencia de claridad. El croma pondera piel, cabello e iris y reajusta los pesos cuando falta la muestra del iris.</p>
</main>

---
layout: none
class: thesis-slide formula-slide
title: 'SELECCIÓN DE LA SUBESTACIÓN'
transition: slide-up
clicks: 1
---

<main class="frame">
  <h1 class="slide-title">SELECCIÓN DE LA SUBESTACIÓN</h1>
  <p class="formula-subtitle">Distancia a los perfiles de referencia</p>
  <QuestionCarousel class="formula-carousel" label="Distancia a los perfiles de referencia" :items="['Fórmula 1', 'Fórmula 2']">
    <template #item-0>
      <math class="formula-long" display="block"><mrow><msub><mi>d</mi><mi>j</mi></msub><mo>=</mo><msqrt><mrow><munderover><mo>∑</mo><mrow><mi>i</mi><mo>=</mo><mn>1</mn></mrow><mn>4</mn></munderover><msub><mi>w</mi><mi>i</mi></msub><msup><mrow><mo>(</mo><mfrac><mrow><msub><mi>x</mi><mi>i</mi></msub><mo>−</mo><msub><mi>p</mi><mrow><mi>j</mi><mo>,</mo><mi>i</mi></mrow></msub></mrow><msub><mi>s</mi><mi>i</mi></msub></mfrac><mo>)</mo></mrow><mn>2</mn></msup></mrow></msqrt></mrow></math>
    </template>
    <template #item-1>
      <math display="block"><mrow><msup><mi>j</mi><mo>∗</mo></msup><mo>=</mo><mrow><munder><mo>arg min</mo><mrow><mi>j</mi><mo>∈</mo><mo>{</mo><mn>1</mn><mo>,</mo><mo>…</mo><mo>,</mo><mn>12</mn><mo>}</mo></mrow></munder><msub><mi>d</mi><mi>j</mi></msub></mrow></mrow></math>
    </template>
  </QuestionCarousel>
  <p class="formula-caption">Se elige el perfil con menor distancia. Cada indicador pesa 0,25. La escala es 0,75 para la calidez y 25 para los demás.</p>
</main>

---
layout: none
class: thesis-slide 
title: 'ASPECTOS LEGALES'
transition: slide-left
---

<SlideFrame>
<h1 class="slide-title">ASPECTOS LEGALES</h1>
<div class="gridcards">
  <div class="glass" style="--card-order:0"><h3>Privacidad</h3><CardText text="Constitución Nacional, artículo 33." :card-order="0" /></div>
  <div class="glass" style="--card-order:1"><h3>Datos personales</h3><CardText text="Ley N.º 7593/2025 y Ley N.º 1682/2001." :card-order="1" /></div>
  <div class="glass" style="--card-order:2"><h3>Derechos de autor</h3><CardText text="Ley N.º 1328/1998 y licencias de software." :card-order="2" /></div>
  <div class="glass" style="--card-order:3"><h3>Ética en el uso de IA</h3><CardText text="Consentimiento, información sobre el tratamiento de imágenes y criterio humano." :card-order="3" /></div>
</div>
</SlideFrame>

---
layout: none
class: thesis-slide chapter-slide
title: 'MARCO METODOLÓGICO'
transition: slide-down
---

<main class="frame">
<ChapterHeading label="CAPÍTULO III" title="MARCO METODOLÓGICO" />
</main>

---
layout: none
class: thesis-slide 
title: 'MARCO METODOLÓGICO'
transition: slide-right
clicks: 5
---

<main class="frame">
<h1 class="slide-title">MARCO METODOLÓGICO</h1>
<QuestionCarousel label="Marco metodológico" :items='[
  {"title":"Tipo de investigación","text":"Aplicada, descriptiva y longitudinal."},
  {"title":"Enfoque","text":"Mixto, con componente cualitativo de orientación fenomenológica."},
  {"title":"Diseño","text":"Preexperimental. Un grupo con preprueba y posprueba."},
  {"title":"Población","text":"51 personas de Lady Di Modas."},
  {"title":"Muestra","text":"50 clientas habituales y la propietaria."},
  {"title":"Muestreo","text":"Censal. Incluyó a toda la población delimitada."}
]' />
</main>

---
layout: none
class: thesis-slide 
title: 'INSTRUMENTOS DE RECOLECCIÓN DE DATOS'
transition: slide-up
clicks: 2
---

<main class="frame">
<h1 class="slide-title">INSTRUMENTOS DE RECOLECCIÓN DE DATOS</h1>
<VerticalCarousel label="Instrumentos de recolección de datos" :items='[
  { "title": "Entrevista", "icon": "chat", "text": "Perspectiva de la propietaria." },
  { "title": "Encuesta inicial", "icon": "checklist", "text": "Dificultades y criterios cromáticos antes de usar el sistema." },
  { "title": "Encuesta final", "icon": "completed", "text": "Percepciones de las clientas después de usar Chroma Sense." }
]' />
</main>

---
layout: none
class: thesis-slide chapter-slide
title: 'RESULTADOS Y DISCUSIÓN'
transition: slide-left
---

<main class="frame">
<ChapterHeading label="CAPÍTULO IV" title="RESULTADOS Y DISCUSIÓN" />
</main>

---
layout: none
class: thesis-slide 
title: 'RESULTADOS – ENTREVISTA'
transition: slide-down
clicks: 4
---

<main class="frame">
<h1 class="slide-title">RESULTADOS – ENTREVISTA</h1>
<VerticalCarousel label="Entrevista a la propietaria de Lady Di Modas" quote :items='[
  {
    "title": "¿Considera usted que las clientas tardan mucho tiempo en decidir qué prendas o colores llevar?",
    "text": "Generalmente"
  },
  {
    "title": "¿La indecisión de las clientas genera dificultades o retrasos en el proceso de venta de la tienda?",
    "text": "Frecuentemente la verdad, en especial las más jóvenes"
  },
  {
    "title": "¿Dispone la tienda actualmente de computadoras, tablets o smartphones para el apoyo a las ventas?",
    "text": "Si disponemos, de una computadora y mi smartphone"
  },
  {
    "title": "¿Considera útil que un sistema de inteligencia artificial recomiende colores a las clientas basándose en sus rasgos físicos?",
    "text": "Si, considero útil la verdad, suena bastante interesante"
  },
  {
    "title": "¿Estaría dispuesta a realizar pruebas en esta plataforma web para automatizar el asesoramiento de imagen de su local?",
    "text": "Si, estoy dispuesta"
  }
]' />
</main>

<!--
Entrevista a la propietaria de Lady Di Modas. Las respuestas se citan literalmente del capítulo IV, §4.1.1–4.1.5.
-->

---
layout: none
class: thesis-slide survey-slide
title: 'RESULTADOS – ENCUESTA INICIAL'
transition: slide-right
---

<main class="frame">
<h1 class="slide-title">RESULTADOS – ENCUESTA INICIAL</h1>
<p class="survey-question">HE ABANDONADO UNA COMPRA POR NO ESTAR SEGURA DE CÓMO ME QUEDA EL COLOR</p>
<LikertChart :counts="[24, 11, 4, 5, 6]" />
</main>

---
layout: none
class: thesis-slide survey-slide
title: 'RESULTADOS – ENCUESTA INICIAL'
transition: slide-up
---

<main class="frame">
<h1 class="slide-title">RESULTADOS – ENCUESTA INICIAL</h1>
<p class="survey-question">SÉ IDENTIFICAR CORRECTAMENTE SI MI SUBTONO DE PIEL ES FRÍO O CÁLIDO.</p>
<LikertChart :counts="[8, 6, 7, 18, 11]" />
</main>

---
layout: none
class: thesis-slide survey-slide
title: 'RESULTADOS – ENCUESTA INICIAL'
transition: slide-left
---

<main class="frame">
<h1 class="slide-title">RESULTADOS – ENCUESTA INICIAL</h1>
<p class="survey-question">PREFIERO RECIBIR ASESORÍA TÉCNICA OBJETIVA ANTES QUE UNA OPINIÓN SUBJETIVA.</p>
<LikertChart :counts="[23, 15, 7, 3, 2]" />
</main>

---
layout: none
class: thesis-slide survey-slide
title: 'RESULTADOS – ENCUESTA FINAL'
transition: slide-down
---

<main class="frame">
<h1 class="slide-title">RESULTADOS – ENCUESTA FINAL</h1>
<p class="survey-question">LOS COLORES RECOMENDADOS POR LA PLATAFORMA CHROMA SENSE COINCIDEN CON MI PERFIL ESTÉTICO.</p>
<LikertChart :counts="[26, 15, 7, 2, 0]" />
</main>

---
layout: none
class: thesis-slide survey-slide
title: 'RESULTADOS – ENCUESTA FINAL'
transition: slide-right
---

<main class="frame">
<h1 class="slide-title">RESULTADOS – ENCUESTA FINAL</h1>
<p class="survey-question">LA PALETA DE COLORES SUGERIDA POR LA PLATAFORMA CHROMA SENSE RESALTÓ MIS RASGOS FÍSICOS PERSONALES</p>
<LikertChart :counts="[24, 18, 5, 3, 0]" />
</main>

---
layout: none
class: thesis-slide survey-slide
title: 'RESULTADOS – ENCUESTA FINAL'
transition: slide-up
---

<main class="frame">
<h1 class="slide-title">RESULTADOS – ENCUESTA FINAL</h1>
<p class="survey-question">EL USO DE LA PLATAFORMA CHROMA SENSE REDUJO MI TIEMPO DE DUDA EN LA TIENDA</p>
<LikertChart :counts="[30, 13, 5, 1, 1]" />
</main>

---
layout: none
class: thesis-slide
title: 'VISIÓN GENERAL / DIAGRAMA'
transition: slide-left
---

<main class="frame">
<h1 class="slide-title">VISIÓN GENERAL / DIAGRAMA</h1>
<ChromaSystemDiagram />
</main>

<!--
El administrador interactúa con los cuatro módulos. Las clientas participan en la encuesta previa, el análisis de colorimetría y las encuestas y el feedback.
-->

---
layout: none
class: thesis-slide
title: 'DIAGRAMA ENTIDAD–RELACIÓN'
transition: slide-down
---

<main class="frame">
<h1 class="slide-title">DIAGRAMA ENTIDAD–RELACIÓN</h1>
<ChromaDer />
</main>

<!--
Figura 86 de la tesis. Abrir el diagrama en una pestaña nueva para ampliar los campos y las relaciones si es necesario.
-->

---
layout: none
class: thesis-slide chapter-slide
title: 'DEMOSTRACIÓN DEL SISTEMA'
transition: slide-right
clicks: 1
---

<main class="frame">
  <div class="chapter">
    <h1>DEMOSTRACIÓN DEL SISTEMA</h1>
    <LiveDemoLink />
  </div>
</main>

<!--
Pulsar Siguiente o hacer clic en ChromaSense para abrir la web en una pestaña nueva. Recorrer el flujo de análisis con una fotografía de prueba y regresar a la presentación para continuar.
-->

---
layout: none
class: thesis-slide 
title: 'DISCUSIÓN'
transition: slide-up
---

<main class="frame">
<h1 class="slide-title">DISCUSIÓN</h1>
<DiscussionDashboard
  :metrics='[
    { "value": 70, "stage": "Encuesta inicial", "description": "Había abandonado una compra por dudas sobre el color." },
    { "value": 86, "stage": "Encuesta final", "description": "Percibió menos tiempo de indecisión al elegir prendas." },
    { "value": 80, "stage": "Encuesta final", "description": "Manifestó mayor seguridad al seleccionar prendas." }
  ]'
/>
</main>

---
layout: none
class: thesis-slide 
title: 'CONCLUSIONES'
transition: slide-left
---

<main class="frame">
<h1 class="slide-title">CONCLUSIONES</h1>
<AnimatedTextCards :items='[
  { "title": "Problema", "text": "Las clientas describieron dudas, desconocimiento cromático e indecisión." },
  { "title": "Solución", "text": "Chroma Sense orienta la elección de colores mediante recomendaciones personalizadas." },
  { "title": "Valoración", "text": "Las clientas percibieron mayor seguridad y menos indecisión." }
]' />
</main>

---
layout: none
class: thesis-slide 
title: 'RECOMENDACIONES'
transition: slide-down
---

<main class="frame">
<h1 class="slide-title">RECOMENDACIONES</h1>
<AnimatedTextCards :items='[
  { "title": "Integración", "text": "Conectar con inventario y sistemas de punto de venta." },
  { "title": "Ampliación", "text": "Explorar morfología corporal y otros criterios de estilo." },
  { "title": "Evaluación", "text": "Estudiar el impacto en otros establecimientos." }
]' />
</main>

---
layout: none
class: thesis-slide budget-slide
title: 'PRESUPUESTO DEL SISTEMA'
transition: slide-right
---

<main class="frame">
  <h1 class="slide-title">PRESUPUESTO DEL SISTEMA</h1>
  <div class="budget-summary"><strong>Gs. 6.875.000</strong><span>275 horas estimadas</span></div>
  <div class="glass budget-table">
    <table aria-label="PRESUPUESTO DEL SISTEMA">
      <thead><tr><th scope="col">Actividad</th><th scope="col">Horas</th><th scope="col">Costo (Gs.)</th><th scope="col">Descripción</th></tr></thead>
      <tbody>
        <tr><th scope="row">Reunión inicial y análisis de requisitos</th><td>12</td><td>300.000</td><td>Entrevista a la propietaria y definición del problema y los requisitos.</td></tr>
        <tr><th scope="row">Diseño de la arquitectura del sistema</th><td>20</td><td>500.000</td><td>Estructura de la aplicación, base PostgreSQL y diagramas.</td></tr>
        <tr><th scope="row">Desarrollo del sistema web</th><td>90</td><td>2.250.000</td><td>Interfaz con React y Vite, backend con Flask y base de datos.</td></tr>
        <tr><th scope="row">Módulo de visión artificial y Machine Learning</th><td>50</td><td>1.250.000</td><td>Procesamiento de imágenes con OpenCV y MediaPipe para el análisis cromático.</td></tr>
        <tr><th scope="row">Integración de inteligencia artificial</th><td>20</td><td>500.000</td><td>API de Gemini para recomendar colores y vestimentas.</td></tr>
        <tr><th scope="row">Pruebas y depuración</th><td>30</td><td>750.000</td><td>Verificación de la plataforma, pruebas de captura y corrección de errores.</td></tr>
        <tr><th scope="row">Aplicación y análisis de encuestas</th><td>25</td><td>625.000</td><td>Encuestas inicial y final a 50 clientas e interpretación de resultados.</td></tr>
        <tr><th scope="row">Despliegue del sistema</th><td>8</td><td>200.000</td><td>Configuración del entorno y puesta en funcionamiento.</td></tr>
        <tr><th scope="row">Capacitación y documentación</th><td>20</td><td>500.000</td><td>Documentación técnica, manuales y orientación de uso.</td></tr>
      </tbody>
    </table>
  </div>
  <p class="budget-caption">Recursos humanos para el desarrollo y la evaluación del sistema.</p>
</main>

<!--
Anexo VI, tabla 57.
-->

---
layout: none
class: thesis-slide budget-slide
title: 'PRESUPUESTO DE LA INVESTIGACIÓN'
transition: slide-up
---

<main class="frame">
  <h1 class="slide-title">PRESUPUESTO DE LA INVESTIGACIÓN</h1>
  <div class="budget-summary"><strong>Gs. 7.550.000</strong><span>Total estimado</span></div>
  <div class="glass budget-table">
    <table aria-label="PRESUPUESTO DE LA INVESTIGACIÓN">
      <thead><tr><th scope="col">Rubro</th><th scope="col">Costo (Gs.)</th><th scope="col">Descripción</th></tr></thead>
      <tbody>
        <tr><th scope="row">Material e insumos</th><td>750.000</td><td>Impresión de instrumentos de recolección, documentos de trabajo y copias para revisiones.</td></tr>
        <tr><th scope="row">Tutoría</th><td>4.850.000</td><td>Mensualidades y matrícula.</td></tr>
        <tr><th scope="row">Viáticos</th><td>450.000</td><td>Traslados para aplicar encuestas, recopilar información y realizar verificaciones.</td></tr>
        <tr><th scope="row">Otros gastos</th><td>1.500.000</td><td>Impresión de los ejemplares del trabajo final para su presentación.</td></tr>
      </tbody>
    </table>
  </div>
  <p class="budget-caption">Costo estimado de la investigación y los materiales del proyecto.</p>
</main>

<!--
Anexo VI, tabla 58.
-->

---
layout: none
class: thesis-slide chapter-slide
title: 'GRACIAS POR SU ATENCIÓN'
transition: slide-left
---

<main class="frame">
<ClosingThanks />
</main>
