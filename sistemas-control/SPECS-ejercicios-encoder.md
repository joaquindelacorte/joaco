# SPECS: Sección "Ejercicios Resueltos" en simulador-encoder.html

**Archivo a modificar:** `sistemas-control/simulador-encoder.html`
**Acción:** Agregar nueva sección al final de la página, antes del cierre `</body>`

---

## Objetivo
Agregar una sección educativa con los ejercicios tipo parcial del Ing. Tirabasso, resueltos paso a paso con los valores numéricos, y con botones que cargan esos valores directamente en el simulador.

---

## Contenido de los ejercicios (extraído del PDF "Ejercicios Tipo para el Parcial")

### Sección A — Conceptos Básicos (20 pts)

**A.1 (10 pts) — Termostato**
Un termostato controla temperatura de una habitación. Setpoint = 18°C, temperatura sube a 22°C.
- a) ¿Es lazo abierto o cerrado? ¿Por qué?
- b) ¿Cuál es el error del sistema?
- c) ¿Qué pasa si entra luz solar directa? ¿Cómo reacciona el control?

**A.2 (10 pts) — Función de Transferencia**
G(s) = 3 / (2s + 1)
- a) ¿Cuál es el valor en estado estacionario ante escalón unitario?
- b) ¿Cuánto tarda en alcanzar el 63% de ese valor?
- c) ¿El sistema es más rápido o más lento que uno con τ = 2?

---

### Sección B — Sistemas de 1er Orden (25 pts)

**B.1 (12 pts) — Circuitos RC** ← VINCULADO AL SIMULADOR
```
Circuito 1: R = 1 kΩ,  C = 1000 µF
Circuito 2: R = 10 kΩ, C = 1000 µF
```
- a) Calcular τ para ambos circuitos. Indicar cuál responde más rápido.
- b) Escribir la función de transferencia (sin calculadora).
- c) Entrada de 5 V. ¿En cuánto tiempo se carga al ~95%?

**Resolución:**
```
Circuito 1: τ₁ = 1000 Ω × 1000×10⁻⁶ F = 1.0 s
Circuito 2: τ₂ = 10000 Ω × 1000×10⁻⁶ F = 10.0 s

H(s) = 1 / (τs + 1)

Circuito 1 → H(s) = 1 / (s + 1)
Circuito 2 → H(s) = 1 / (10s + 1)

t_95% ≈ 3τ
  Circuito 1: t = 3 × 1.0 s = 3.0 s
  Circuito 2: t = 3 × 10.0 s = 30.0 s
```

**B.2 (13 pts) — Temperatura**
Sistema térmico: temperatura inicial 20°C, calienta hasta estado estacionario de 80°C, τ = 5 min
- a) ¿Cuánto vale τ en segundos?
- b) ¿A qué tiempo se alcanza 79°C?
- c) Aproximar con 5 constantes de tiempo → valor final.

**Resolución:**
```
τ = 5 min = 300 s

v(t) = 80 × (1 - e^(-t/300))

Para v(t) = 79:
  79 = 80 × (1 - e^(-t/300))
  e^(-t/300) = 1/80
  t = 300 × ln(80) ≈ 1330 s ≈ 22.2 min

5τ = 1500 s → v(1500) = 80 × (1 - e^(-5)) ≈ 79.46°C
```

---

### Sección C — Polos y Estabilidad (20 pts)

**C.1 (10 pts)**
```
G1(s) = 1 / (s + 2)   → polo en s = -2
G2(s) = 1 / (s - 2)   → polo en s = +2
G3(s) = 1 / (s² + 2s + 5) → polos en s = -1 ± 2j
```
- a) ¿Cuáles son estables?
- b) Dibujar polos en plano complejo
- c) Con G3 y ganancia K = 10, ¿sigue siendo estable?

**Resolución:**
```
G1: polo en semiplano izquierdo (Re = -2) → ESTABLE ✓
G2: polo en semiplano derecho (Re = +2)  → INESTABLE ✗
G3: polos complejos con Re = -1          → ESTABLE ✓

G3 con K=10: la planta no cambia (lazo abierto).
En lazo cerrado 1+KG(s)=0 → s²+2s+5+10=0 → s²+2s+15=0
Discriminante: 4 - 60 < 0 → polos imaginarios puros con Re > 0... 
No, raíces: s = (-2 ± √(4-60))/2 = -1 ± j√14 → Re = -1 < 0 → AÚN ESTABLE ✓
```

**C.2 (10 pts) — Mapa de Polos**
Datos del gráfico: polos en s = -1+2j, s = -1-2j, s = -3
- a) ¿Estable?
- b) ¿Cuál polo domina la respuesta? ¿Por qué?
- c) Una respuesta más rápida implicaría mover los polos hacia...

**Resolución:**
```
Todos los polos tienen Re < 0 → ESTABLE ✓
Polo dominante: s = -1 ± 2j (más cercano al eje imaginario → τ más grande → más lento)
s = -3 decae 3 veces más rápido y casi no se ve en la respuesta final.
Para respuesta más rápida: alejar polos del eje imaginario (más a la izquierda).
```

---

### Sección D — Control On-Off y Proporcional (20 pts)

**D.1 (10 pts)**
Planta: G(s) = 1 / (s + 1). Bomba de agua: u=0 (apagada) o u=2 L/s.
Controlador proporcional: Kp = 3.
- a) ¿Qué pasa con On-Off? ¿A qué nivel se regula?
- b) Con control proporcional, ¿cuál es el nivel de equilibrio?
- c) ¿Para qué Kp se minimiza el error?

**Resolución:**
```
On-Off: oscila alrededor del setpoint (ciclo continuo encendido/apagado).
Proporcional con Kp=3:
  Error en estado estacionario = 1/(1+Kp×G(0)) = 1/(1+3×1) = 0.25
  Nivel de equilibrio → hay error permanente (offset).
Para reducir error: aumentar Kp → mayor acción proporcional,
  pero riesgo de oscilación y sobreimpulso.
```

**D.2 (10 pts)**
G(s) = 1/(s+1), respuesta a escalón con distintos controladores.
- a) Con On-Off: describir forma de la respuesta
- b) Con P: ¿hay sobreimpulso? ¿error permanente?
- c) Con PI: ¿qué pasa con el sobreimpulso y el tiempo de establecimiento?
- d) Con PID: ¿qué ventaja agrega la D?

**Resolución:**
```
On-Off: oscilación cuadrada alrededor del setpoint.
P: sin sobreimpulso (planta 1er orden), pero error permanente en estado estacionario.
PI: elimina error permanente (integrador), puede aumentar levemente el sobreimpulso.
PID: la acción derivativa anticipa cambios → reduce sobreimpulso, acelera la respuesta.
```

---

### Sección E — Simulación con Octave (15 pts)

**E.1**
Planta: G(s) = 1/(s+1), Controlador proporcional Kp=2, escalón unitario.
- a) Graficar respuesta al escalón
- b) Calcular valor final y error
- c) Repetir con Kp=5 y Kp=10 → comparar

**Resolución:**
```
Lazo cerrado: T(s) = Kp×G(s) / (1 + Kp×G(s)) = Kp/(s+1+Kp)

Con Kp=2:  T(s) = 2/(s+3)  → τ_cl = 1/3 s,  y_ss = 2/3 ≈ 0.667
Con Kp=5:  T(s) = 5/(s+6)  → τ_cl = 1/6 s,  y_ss = 5/6 ≈ 0.833
Con Kp=10: T(s) = 10/(s+11) → τ_cl = 1/11 s, y_ss = 10/11 ≈ 0.909

A mayor Kp: respuesta más rápida y error más pequeño, pero sin PI nunca llega a 1.
```

---

## Diseño de la sección en HTML

### Nombre de la sección
`🎯 Ejercicios Tipo — Parcial Ing. Tirabasso`

### Estructura visual
- Misma navbar/tabs existente — agregar esta sección como nueva sub-sección dentro de la página (no tab nuevo, scroll continuo)
- Subtítulo tipo `.stitle` igual al resto del HTML
- Cada ejercicio en una `.card` expandible (accordion con `<details>/<summary>`)
- Dentro de cada card:
  - **Enunciado** en texto normal
  - **Resolución paso a paso** en bloque `.fbox` (igual al resto del simulador)
  - Donde aplique: botón verde **"Cargar en simulador"** que setea los sliders

### Ejercicios con botón "Cargar en simulador"

**B.1 Circuito 1** → botón carga: R=1000Ω, C=1000µF (=1000000nF), n=1000, N=100
**B.1 Circuito 2** → botón carga: R=10000Ω, C=1000µF, n=1000, N=100
**B.2 Térm.** → botón carga: R equivalente para τ=300s (mostrar nota "τ=RC, ajustá C para τ=300s")

Los botones deben:
1. Setear los sliders a los valores del ejercicio
2. Forzar re-render del osciloscopio y métricas
3. Hacer scroll suave al simulador (`#simulador` o elemento canvas)

### Tag/badge del ejercicio
Cada card tiene un badge:
- `📐 Geometría` / `⚡ Circuito RC` / `📊 Estabilidad` / `🎛️ Control` / `💻 Octave`

---

## Restricciones
- NO romper nada del simulador existente
- Los botones "Cargar en simulador" deben funcionar aunque el simulador esté scrolleado fuera de vista
- Mismos colores/tipografía del resto del HTML
- Los bloques de resolución deben tener el mismo estilo `.fbox-nums` (fondo verde) ya usado en el HTML
