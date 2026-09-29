# SPECS — Apuntes Hub (página independiente + nav entre apuntes)

**Creado por:** proyectos-bot  
**Fecha:** 2026-09-22  
**Repo:** `C:/Users/Joaquin De La Corte/proyectos/joaco/` → GitHub: `joaquindelacorte/joaco`

---

## Resumen ejecutivo

Dos entregables en una sola tarea:

1. **`apuntes/index.html`** — página independiente de acceso rápido a todos los apuntes, mobile-first, que funciona como hub sin depender del portafolio principal.
2. **Nav inter-apuntes** — agregar en cada página de apuntes existente una barra de navegación fija (o footer) que permita ir al Hub, volver al portafolio y saltar a cualquier otra materia.

---

## Entregable 1 — `apuntes/index.html`

### Propósito
Página standalone para acceso rápido desde móvil o bookmark directo. URL resultante: `joacodelacorte.netlify.app/apuntes/` (Netlify sirve index.html del directorio).

### Estilo / Design system
- Seguir **exactamente** el mismo design system que `index.html` del portafolio:
  - Fuentes: `Archivo` (headings), `Inter` (body), `JetBrains Mono` (badges/chips) — Google Fonts
  - Variables CSS del portafolio: `--bg`, `--surface`, `--ink`, `--ink-2`, `--amber`, `--teal`, `--indigo`, etc.
  - Todo CSS **inline en `<style>`** — sin archivos externos
- Dark theme base (igual al portafolio)
- El único archivo a crear es `apuntes/index.html` — self-contained

### Estructura del HTML

```
<head>
  charset, viewport, SEO básico
  Google Fonts (Archivo + Inter + JetBrains Mono)
  <style> inline con todas las reglas </style>
</head>
<body>
  <!-- HEADER -->
  Header fijo con:
    - Logo/nombre: "Apuntes · Joaco" (link a joacodelacorte.netlify.app)
    - Link "← Portafolio" a la derecha

  <!-- HERO -->
  <section class="hero">
    eyebrow chip teal: "Carrera"
    h1: "Cuaderno de la facultad"
    p: "Automatización y Control · Universidad de Pilar. Teoría, ejercicios y simuladores por materia."

  <!-- MATERIAS GRID -->
  <section class="materias">
    Una card por materia (ver lista abajo).
    Cada card tiene:
      - Color de acento de la materia (ver palette)
      - Nombre de la materia (bold)
      - N páginas disponibles (ej: "3 apuntes")
      - Links individuales a cada página (lista compacta)
      - En mobile: card ocupa ancho completo; en desktop: grid 2 o 3 col

  <!-- FOOTER -->
  footer: "Joaquín De La Corte · joacodelacorte.netlify.app"
</body>
```

### Organización por cuatrimestres

La página se divide en **5 secciones**, una por cuatrimestre. Cada sección tiene:
- Badge de estado: `✅ Aprobado` / `🔵 Cursando` / `⬜ Próximo`
- Cards de las materias del cuatrimestre

**Regla de cards desactivadas:** materias sin apuntes en el repo se renderizan en escala de grises (no color), sin links, con texto "Sin apuntes aún" en lugar de los links. El cursor es `default` (no pointer). No son clickeables.

```css
.materia-card--disabled {
  filter: grayscale(1);
  opacity: .45;
  pointer-events: none;
  border-left-color: #4b5563;
}
.materia-card--disabled h3 { color: #6b7280; }
.materia-card--disabled .no-apuntes {
  font-size: .78rem;
  color: #6b7280;
  font-style: italic;
  font-family: 'JetBrains Mono', monospace;
}
```

---

### Cuatrimestre 1 — 1er Año | ✅ Aprobado

> Todas desactivadas (sin apuntes en repo)

| Materia | Estado |
|---|---|
| Introducción a la Automatización | desactivada |
| Elementos para la Comprensión de Lengua Extranjera | desactivada |
| Fundamentos de la Programación | desactivada |
| Elementos de Matemática | desactivada |
| Introducción a la Cultura Digital | desactivada |

---

### Cuatrimestre 2 — 1er Año | ✅ Aprobado

> Todas desactivadas (sin apuntes en repo)

| Materia | Estado |
|---|---|
| Mecánica de la Robótica | desactivada |
| Programación Estructurada | desactivada |
| Neumática | desactivada |
| Sistemas de Representación | desactivada |
| Taller de Lectura y Escritura Académica | desactivada |

---

### Cuatrimestre 3 — 2do Año | ✅ Aprobado

> Los href deben ser **relativos desde `apuntes/`**, es decir `../sistemas-control/teoria.html`.

| Materia | Color acento | Páginas y hrefs (desde apuntes/) |
|---|---|---|
| Robótica I | `#dc2626` (rojo) | `../robotica/teoria.html` "Teoría" |
| Análisis Matemático I | `#7c3aed` (violeta) | `../analisis-matematico/teoria-1.html` "Teoría 1", `../analisis-matematico/teoria-2.html` "Teoría 2", `../analisis-matematico/teoria-3.html` "Teoría 3", `../analisis-matematico/regla-de-la-cadena.html` "Regla de la cadena", `../analisis-matematico/parcial2.html` "Parcial 2", `../analisis-matematico/parcial2-modelo.html` "Modelo P2", `../analisis-matematico/parcial2-express.html` "Express P2", `../analisis-matematico/parcial2-autoevaluacion.html` "Autoevaluación" |
| Electrotecnia | `#d97706` (amber) | `../electrotecnia/teoria.html` "Teoría" |
| Estadística | `#059669` (esmeralda) | `../estadistica/teoria.html` "Teoría", `../estadistica/resumen.html` "Resumen", `../estadistica/parcial1.html` "Parcial 1", `../estadistica/parcial2.html` "Parcial 2", `../estadistica/repaso-parcial2.html` "Repaso P2", `../estadistica/simulacro-parcial2-explicado.html` "Simulacro P2 explicado" |
| Hidráulica | `#0891b2` (cyan) | `../hidraulica/teoria.html` "Teoría", `../hidraulica/parcial2.html` "Parcial 2" |

---

### Cuatrimestre 4 — 2do Año | 🔵 Cursando actualmente

| Materia | Color acento | Páginas y hrefs (desde apuntes/) |
|---|---|---|
| Automatización Industrial | `#16a34a` (verde) | `../automatizacion-industrial/logica-digital.html` "Lógica Digital" |
| Sistemas de Control | `#3730a3` (indigo) | `../sistemas-control/teoria.html` "Teoría", `../sistemas-control/simulador-encoder.html` "Simulador Encoder", `../sistemas-control/pid-horno.html` "PID Horno" |
| Controladores Lógicos Programables | desactivada | — |
| Álgebra | `#2563eb` (azul) | `../algebra-lineal/teoria.html` "Teoría", `../algebra-lineal/teoria-unidad2.html` "Unidad 2" |
| Taller Sociocomunitario | `#0d9488` (teal) | `../taller-sociocomunitario/teoria.html` "Teoría" |

---

### Cuatrimestre 5 — 3er Año | ⬜ Próximo

> Todas desactivadas (sin apuntes en repo)

| Materia | Estado |
|---|---|
| Robótica II | desactivada |
| Microprocesadores | desactivada |
| Seminario a Elección I | desactivada |
| Práctica Profesional | desactivada |
| Experiencias Formativas Acreditables (EFA) | desactivada |

### Diseño de card (detalle)

```css
/* cada card */
.materia-card {
  border-left: 3px solid var(--acento);
  background: var(--surface);
  border-radius: 8px;
  padding: 1rem 1.25rem;
}
.materia-card h3 { color: var(--acento); font-family: Archivo; }
.materia-card .count { font-size: .75rem; font-family: JetBrains Mono; color: var(--ink-2); }
.materia-links a {
  display: inline-block;
  margin: .25rem .25rem 0 0;
  padding: .2rem .6rem;
  border-radius: 4px;
  background: color-mix(in srgb, var(--acento) 12%, transparent);
  color: var(--acento);
  font-size: .8rem;
  text-decoration: none;
}
.materia-links a:hover { background: color-mix(in srgb, var(--acento) 25%, transparent); }
```

### Grid responsive

```css
.materias-grid {
  display: grid;
  grid-template-columns: 1fr;          /* mobile: 1 col */
  gap: 1rem;
}
@media (min-width: 640px) {
  .materias-grid { grid-template-columns: repeat(2, 1fr); }
}
@media (min-width: 1024px) {
  .materias-grid { grid-template-columns: repeat(3, 1fr); }
}
```

---

## Entregable 2 — Nav inter-apuntes en páginas existentes

### Qué agregar

En **cada una** de las 24 páginas de apuntes existentes (listadas abajo), agregar:

1. **Barra superior fija** (`position: sticky; top: 0`) con:
   - `← Portafolio` → link a `https://joacodelacorte.netlify.app/#apuntes`
   - `Hub Apuntes` → link relativo al `apuntes/index.html` desde cada página (cálculo de profundidad: todas están a 1 nivel del root, entonces `../apuntes/`)
   - Nombre de la materia actual (texto, no link)

2. **Footer de navegación** al final del `<body>` con links a las otras páginas de la **misma materia** (si hay más de una). No listar todas las materias — solo el contexto inmediato.

### Páginas a modificar

```
analisis-matematico/teoria-1.html
analisis-matematico/teoria-2.html
analisis-matematico/teoria-3.html
analisis-matematico/regla-de-la-cadena.html
analisis-matematico/parcial2.html
analisis-matematico/parcial2-modelo.html
analisis-matematico/parcial2-express.html
analisis-matematico/parcial2-autoevaluacion.html
algebra-lineal/teoria.html
algebra-lineal/teoria-unidad2.html
electrotecnia/teoria.html
estadistica/teoria.html
estadistica/resumen.html
estadistica/parcial1.html
estadistica/parcial2.html
estadistica/repaso-parcial2.html
estadistica/simulacro-parcial2-explicado.html
hidraulica/teoria.html
hidraulica/parcial2.html
robotica/teoria.html
sistemas-control/teoria.html
sistemas-control/simulador-encoder.html
sistemas-control/pid-horno.html
automatizacion-industrial/logica-digital.html
taller-sociocomunitario/teoria.html
```

### Estilo de la barra de nav

```html
<!-- PEGAR INMEDIATAMENTE DESPUÉS DE <body>, ANTES de cualquier contenido existente -->
<div class="apuntes-nav">
  <a href="https://joacodelacorte.netlify.app/#apuntes" class="apuntes-nav__back">← Portafolio</a>
  <a href="../apuntes/" class="apuntes-nav__hub">Hub Apuntes</a>
  <span class="apuntes-nav__current">[Nombre materia]</span>
</div>
```

```css
/* PEGAR en el <style> existente (o en un bloque nuevo justo antes de </head>) */
.apuntes-nav {
  position: sticky;
  top: 0;
  z-index: 100;
  display: flex;
  align-items: center;
  gap: .75rem;
  padding: .5rem 1rem;
  background: rgba(10,10,18,.92);
  backdrop-filter: blur(8px);
  border-bottom: 1px solid rgba(255,255,255,.08);
  font-family: 'Inter', sans-serif;
  font-size: .82rem;
}
.apuntes-nav a {
  color: #94a3b8;
  text-decoration: none;
  padding: .2rem .5rem;
  border-radius: 4px;
  transition: background .15s;
}
.apuntes-nav a:hover { background: rgba(255,255,255,.07); color: #e2e8f0; }
.apuntes-nav__hub { color: #38bdf8 !important; }
.apuntes-nav__current {
  margin-left: auto;
  color: #64748b;
  font-family: 'JetBrains Mono', monospace;
  font-size: .75rem;
}
@media (max-width: 480px) {
  .apuntes-nav__current { display: none; }
}
```

### Footer intra-materia (solo si hay >1 página en la materia)

```html
<!-- PEGAR ANTES de </body> -->
<nav class="apuntes-footer-nav">
  <span class="apuntes-footer-nav__label">Más de esta materia:</span>
  <!-- links a los otros archivos de la misma carpeta, con texto descriptivo -->
  <a href="teoria-1.html">Teoría 1</a>
  <a href="teoria-2.html" class="active">Teoría 2</a>  <!-- active = página actual -->
  <!-- etc. -->
</nav>
```

```css
.apuntes-footer-nav {
  margin-top: 3rem;
  padding: 1rem 1.25rem;
  background: rgba(255,255,255,.04);
  border-top: 1px solid rgba(255,255,255,.08);
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: .5rem;
  font-family: 'Inter', sans-serif;
  font-size: .83rem;
}
.apuntes-footer-nav__label { color: #64748b; margin-right: .25rem; }
.apuntes-footer-nav a {
  color: #94a3b8;
  text-decoration: none;
  padding: .2rem .6rem;
  border-radius: 4px;
  background: rgba(255,255,255,.06);
}
.apuntes-footer-nav a:hover { background: rgba(255,255,255,.12); color: #e2e8f0; }
.apuntes-footer-nav a.active {
  background: rgba(56,189,248,.15);
  color: #38bdf8;
}
```

---

## También actualizar: `index.html` del portafolio

En la sección `#apuntes` del `index.html` principal, agregar debajo del `notes-grid` un link al hub:

```html
<!-- REEMPLAZAR la línea existente: -->
<div class="sheet__links notes-folder__more"><a href="README.md">Ver índice completo en el README →</a></div>

<!-- POR: -->
<div class="sheet__links notes-folder__more">
  <a href="apuntes/">Ver hub de apuntes →</a>
</div>
```

---

## Constraints técnicos

- **Sin frameworks** ni bundlers. HTML + CSS + JS vanilla únicamente.
- **CSS inline** en `<style>` — nunca archivos externos `.css`. (Patrón del repo.)
- Cada apunte es un archivo standalone. No romper el contenido existente.
- Para las páginas existentes: la barra `.apuntes-nav` se inserta con `position: sticky` para no desplazar el layout actual.
- El color de fondo de la barra usa `rgba` con `backdrop-filter` para que no tape contenido fijo preexistente.
- Verificar que `../apuntes/` resuelve correctamente en Netlify (sí lo hace si existe `apuntes/index.html`).

---

## Orden de implementación sugerido

1. Crear `apuntes/index.html` completo.
2. Modificar las 24 páginas de apuntes (barra + footer intra-materia).
3. Actualizar el link en `index.html` del portafolio.
4. Commit + push a `joaquindelacorte/joaco`.
