# SPECS: Simulador Interactivo de Encoder

**Archivo destino:** `C:/Users/Joaquin De La Corte/proyectos/joaco/sistemas-control/simulador-encoder.html`
**Repo:** `github.com/joaquindelacorte/joaco` — carpeta `sistemas-control/`
**Referencia de estilo:** `teoria.html` (mismas CSS vars, nav, cards, tab-btn pattern)

---

## Objetivo
Herramienta educativa interactiva que modela:
1. Mecánica del disco encoder (geometría, rotación)
2. Generación de señales A/B en cuadratura
3. Degradación de señal por filtro RC (modelo Laplace)
4. Detección de fallo por pérdida de pulsos a alta velocidad

---

## Stack
- HTML5 + CSS (mismo design system de `teoria.html`: `--main:#3730a3`, `--main-lt:#4f46e5`, `--bg:#f5f6fb`, etc.)
- JavaScript puro (sin frameworks)
- **Three.js** (CDN) para vista 3D del disco
- **Chart.js** (CDN) para osciloscopio y Diagrama de Bode
- **Sin dependencias adicionales**

---

## Módulos / Secciones del simulador

### 1. Panel de Control (inputs)
Sliders con valor numérico en tiempo real:

| Slider | Rango | Default | Unidad |
|---|---|---|---|
| RPM (n) | 10 – 10000 | 1000 | RPM |
| PPR (N) | 4 – 10000 | 100 | pulsos/rev |
| Radio (r) | 5 – 100 | 30 | mm |
| Resistencia (R) | 10 – 10000 | 1000 | Ω |
| Capacitancia (C) | 1 – 10000 | 100 | nF |
| V_max | 3.3 – 24 | 5 | V |
| V_IH | 0.5 – V_max | 3.0 | V |
| V_IL | 0 – V_IH | 0.8 | V |

Toggle adicional: **Modo de driver** → `Open Collector` / `Line Driver` (visual only, afecta etiqueta)

---

### 2. Vista 3D del Disco (Three.js)
- Disco circular negro con ranuras blancas distribuidas según PPR
- Rota en tiempo real según RPM (animación `requestAnimationFrame`)
- Cámara levemente inclinada (perspectiva 3D, no ortogonal)
- Efecto LED/sensor: punto de luz naranja fijo sobre la pista de ranuras
- Al pasar por ranura: sensor parpadea en verde; entre ranuras: rojo
- Velocidad visual capped a ~600 RPM para que no sea solo blur

---

### 3. Osciloscopio Virtual (Chart.js, tiempo real)
Dos trazas sobre el mismo gráfico `V vs t`:
- **Traza azul** — V_in(t): onda cuadrada ideal (0 → V_max)
- **Traza naranja** — V_out(t): onda real con carga/descarga RC:
  - Subida: `v_out(t) = V_max * (1 - e^(-t/τ))`
  - Bajada: `v_out(t) = V_max * e^(-t/τ)`
- **Líneas punteadas rojas**: V_IH y V_IL como umbrales horizontales
- Mostrar 3–5 períodos completos en pantalla
- Actualizar en tiempo real al mover sliders

---

### 4. Diagrama de Bode (Chart.js)
Gráfico `|H(jω)| [dB] vs frecuencia [Hz]` — escala log en eje X:
- Traza de la función de transferencia `H(s) = 1/(τs+1)` calculada de f=1Hz a f=1MHz
- Punto de operación actual (`f_pulso`) marcado con un punto rojo vertical
- Frecuencia de corte (`f_c`) marcada con línea vertical punteada
- Label flotante mostrando: `f_pulso = X Hz`, `f_c = Y Hz`, `Atenuación = Z dB`

---

### 5. Panel de Métricas y Alerta
Mostrar en tiempo real, actualizando con cada cambio de slider:

| Métrica | Fórmula |
|---|---|
| f_pulso | `(N × n) / 60` Hz |
| T_pulso | `1 / f_pulso` µs |
| T_alto | `T_pulso / 2` µs |
| τ (tau) | `R × C` µs |
| f_c | `1 / (2π × τ)` Hz |
| 3τ | `3 × R × C` µs |
| d (paso entre ranuras) | `(2π × r) / N` mm |
| w (ancho ventana) | `d / 2` mm |

**Indicador de estado** (semáforo grande):
- 🟢 **OPERACIÓN NORMAL** — `T_alto >= 3τ` Y `V_peak >= V_IH`
- 🟡 **ATENUACIÓN LEVE** — `T_alto >= τ` pero `T_alto < 3τ`
- 🔴 **PÉRDIDA DE CONTEO / ERROR** — `T_alto < τ` O `V_peak < V_IH`

Mostrar también:
- Pulsos ideales/seg vs pulsos detectables/seg (estimados)
- Texto explicativo dinámico que cambia según estado (ej: "A esta velocidad, el capacitor no alcanza a cargarse completamente…")

---

## Fórmulas matemáticas completas

```
d       = (2 × π × r) / N           [mm]
w       = d / 2                      [mm]
Δθ      = 360° / N                  [grados]
f_pulso = (N × n) / 60              [Hz]
T_pulso = 1 / f_pulso               [s]
T_alto  = T_pulso / 2               [s]
τ       = R × C                     [s]
f_c     = 1 / (2 × π × τ)          [Hz]

v_out carga:   V_max × (1 - e^(-t/τ))
v_out descarga: V_max × e^(-t/τ)

V_peak  = V_max × (1 - e^(-T_alto/τ))

H(jω)  = 1 / sqrt(1 + (ω×τ)²)
|H|_dB = 20 × log10(H(jω))
```

---

## Señal en Cuadratura (Canal A y B)
- Canal A: onda cuadrada con f_pulso
- Canal B: igual que A pero desfasada T_pulso/4
- Toggle en panel: **Horario (CW)** / **Antihorario (CCW)**
  - CW: A adelanta a B (B retrasado +90°)
  - CCW: B adelanta a A (A retrasado +90°)
- Mostrar ambos canales en el osciloscopio (A=azul, B=verde, V_out_A=naranja)

---

## Layout de página

```
[NAV igual a teoria.html — misma barra de tabs]

[HERO] Simulador de Encoder Óptico — subtítulo breve

[ROW 1] 
  [LEFT 35%] Panel de Control (sliders + toggle driver + toggle CW/CCW)
  [RIGHT 65%] Vista 3D del disco (Three.js, ~400px height)

[ROW 2 — full width]
  Osciloscopio Virtual (Chart.js, ~300px height)

[ROW 3 — 2 cols]
  [LEFT] Diagrama de Bode
  [RIGHT] Panel de métricas + semáforo de estado

[ROW 4 — full width]
  Cards educativas: Geometría del Disco / Modelo RC / Cuadratura / Criterio de Fallo
  (con las fórmulas renderizadas en bloques `.formula` como en teoria.html)
```

---

## Restricciones / criterios de calidad
- Archivo único `.html` (todo inline: CSS + JS)
- Mobile-first, responsive
- Sliders deben actualizar TODO en tiempo real (sin botón "Calcular")
- Animación 3D no debe trabar la UI — usar `requestAnimationFrame` desacoplado de los gráficos
- Mismos colores/tipografía que `teoria.html`
- Fórmulas en bloques `<code>` o estilo `.formula` como el resto del apunte
- Comentarios en JS explicando cada sección de lógica

---

## Entregable
Archivo `simulador-encoder.html` listo para abrir en browser, ubicado en:
`C:/Users/Joaquin De La Corte/proyectos/joaco/sistemas-control/simulador-encoder.html`
