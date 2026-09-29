# SPECS — Ejercicios Tipo Parcial: Sistemas de Control

**Archivo a crear:** `sistemas-control/ejercicios-parcial.html`
**Repo:** `C:/Users/Joaquin De La Corte/proyectos/joaco/`
**Referencia de estilo:** `sistemas-control/teoria.html` (inline CSS, mismo color `--main:#3730a3` indigo)
**Agregar link en footer nav** de `sistemas-control/teoria.html`

---

## Estructura de la página

Misma arquitectura que los demás archivos de la materia:
- `<!DOCTYPE html>`, charset UTF-8, viewport
- Todo CSS **inline** en `<style>` — no stylesheets externos
- Color `--main: #3730a3` (indigo), mismo que teoria.html
- Mismos tokens CSS: `--bg`, `--card`, `--text`, etc. — copiar del header de teoria.html
- Nav superior con tabs por sección (A, B, C, D, E), uno activo a la vez con clase `active`
- `.page` / `.page.active` para mostrar/ocultar secciones
- Footer nav con link de vuelta a `teoria.html`

---

## Nav tabs

```
📐 Sección A | 🔋 Sección B | 📍 Sección C | 🎛️ Sección D | 💻 Sección E
```

IDs de páginas: `page-a`, `page-b`, `page-c`, `page-d`, `page-e`

---

## Contenido por sección

### Sección A — Conceptos básicos (20 pts)

#### Problema A.1 — Control de temperatura con termostato

**Enunciado:** termostato que enciende calefacción < 18°C y apaga > 22°C.

**a) ¿Lazo abierto o cerrado?**
→ **Lazo cerrado.** El termostato mide continuamente la temperatura (retroalimentación) y decide si actuar. La salida (temperatura) influye sobre la entrada (decisión de encender/apagar).

**b) Identificación de elementos:**
- **Sensor:** termistro o sensor de temperatura del termostato — mide la variable controlada
- **Controlador:** lógica del termostato — compara con el rango (18–22°C) y decide
- **Actuador:** resistencia calefactora / unidad de calefacción — modifica la temperatura

**c) Sin histéresis (conmuta exactamente en 20°C):**
→ El sistema entraría en **chattering**: la calefacción encendería y apagaría continuamente (en ciclos muy cortos) porque cualquier mínima variación alrededor de 20°C dispara la acción. Esto degrada el actuador y genera oscilaciones permanentes sin estabilización real.

---

#### Problema A.2 — G(s) = 3/(2s+1)

**a) Salida en estado estacionario con escalón de amplitud 2:**
Aplicando el teorema del valor final:
```
y_ss = lim[s→0] s · G(s) · (2/s) = G(0) · 2 = (3/1) · 2 = 6
```
**y_ss = 6**

**b) Tiempo para alcanzar el 63% del valor final:**
La constante de tiempo es el denominador del término con s: **τ = 2 segundos**
El 63% del valor final se alcanza exactamente en t = τ = **2 s**

**c) Si se duplica el coeficiente de s → G(s) = 3/(4s+1):**
τ pasa de 2 a 4 segundos → el sistema se vuelve **más lento**.
*Justificación: mayor τ significa que la exponencial decae más despacio; el sistema tarda más en alcanzar el estado estacionario.*

---

### Sección B — Sistemas de 1er orden (25 pts)

#### Problema B.1 — Circuitos RC

**a) Constante de tiempo τ = R·C:**
- Circuito 1: τ₁ = 1 kΩ × 1000 µF = 1000 × 0,001 = **1 s**
- Circuito 2: τ₂ = 10 kΩ × 1000 µF = 10000 × 0,001 = **10 s**

**b) ¿Cuál se carga más rápido?**
El **Circuito 1** (τ₁ = 1 s). Físicamente: con menor resistencia, el capacitor puede recibir más corriente en el mismo tiempo → se carga más rápido. La resistencia limita la velocidad de carga del capacitor.

**c) Gráficos (descripción para renderizar con canvas o inline SVG):**
Dos curvas exponenciales crecientes desde 0 V hasta 5 V (setpoint = escalón 5V):
- Circuito 1 (τ=1s): alcanza ~3,15 V a t=1s, ~4,32 V a t=2s, ~4,97 V a t=5s
- Circuito 2 (τ=10s): alcanza ~0,48 V a t=1s, ~0,90 V a t=2s, ~2,21 V a t=5s

*Mostrar ambas curvas en canvas con leyenda "Circuito 1 (τ=1s)" e "Circuito 2 (τ=10s)". Usar colores: indigo para C1, naranja para C2.*

---

#### Problema B.2 — Termómetro digital (sistema de primer orden)

Datos: sube de 20°C a 80°C (ΔT_total = 60°C). A t=5s, lectura = 58°C → subió 38°C.

**a) Constante de tiempo:**
```
y(t) = ΔT_total · (1 - e^(-t/τ))
38 = 60 · (1 - e^(-5/τ))
e^(-5/τ) = 1 - 38/60 = 0,3667
-5/τ = ln(0,3667) = -1,003
τ ≈ 5 / 1,003 ≈ 5 s
```
**τ ≈ 5 segundos**

**b) Tiempo para llegar a 79°C (sube 59°C):**
```
59 = 60 · (1 - e^(-t/5))
e^(-t/5) = 1/60
t = 5 · ln(60) ≈ 5 · 4,094 ≈ 20,5 s
```
**t ≈ 20,5 s** (~4τ, que corresponde al ~98,2% del valor final)

**c) Punta más gruesa (mayor capacidad térmica):**
La constante de tiempo térmica es τ = R_térmica · C_térmica. Al aumentar la capacidad térmica (C), **τ aumenta** → respuesta más lenta. El termómetro tardará más en reflejar cambios de temperatura.

---

### Sección C — Polos y estabilidad (20 pts)

#### Problema C.1 — Tres funciones de transferencia

```
G₁(s) = 1/(s+2)   →   polo en s = -2   (parte real: -2 < 0) → ESTABLE
G₂(s) = 1/(s-2)   →   polo en s = +2   (parte real: +2 > 0) → INESTABLE
G₃(s) = 1/(s²+2s+5) → polos: s = (-2 ± √(4-20))/2 = -1 ± 2j  (parte real: -1 < 0) → ESTABLE
```

**a) Inestable: G₂(s).** Polo con parte real positiva (s=+2) → la respuesta crece exponencialmente sin límite.

**b) G₃: ¿oscila?**
Sí, **oscila con amortiguamiento**. Los polos son complejos conjugados (-1±2j): la parte imaginaria (±2j) genera oscilación, y la parte real negativa (-1) provoca que esa oscilación decaiga con el tiempo → sistema subamortiguado estable.

**c) G₁ con Kp=10 en lazo cerrado:**
```
T(s) = (10 · 1/(s+2)) / (1 + 10/(s+2)) = 10/(s+2+10) = 10/(s+12)
```
Polo en s = -12 → **sigue siendo estable** (parte real más negativa que el original, de hecho más rápido).

---

#### Problema C.2 — Polos en s = -1 ± 2j

**a) Estabilidad:** Parte real = -1 < 0 → **ESTABLE**

**b) ¿Sobrepaso?** Sí. Polos complejos con parte imaginaria ≠ 0 → respuesta **subamortiguada** → habrá sobrepaso (la salida supera el setpoint antes de estabilizarse).

**c) Polos en -3 ± 2j:**
- **Más rápida:** parte real más negativa → la exponencial decae más rápido → respuesta más veloz
- **Menor sobrepaso:** ω_n = √(9+4) = √13 ≈ 3,6; ζ = 3/√13 ≈ 0,83 (vs. ζ original = 1/√5 ≈ 0,45) → mayor amortiguamiento relativo → **menos sobrepaso**

**d) Mapa de polos:**
Renderizar un plano complejo (eje real horizontal, eje imaginario vertical) con:
- Punto en (-1, +2) → círculo relleno, etiqueta "s₁ = -1+2j"
- Punto en (-1, -2) → círculo relleno, etiqueta "s₂ = -1-2j"
- Región RHP sombreada en rojo claro (parte real > 0 = zona inestable)
- Región LHP en verde muy suave (zona estable)

*Implementar con canvas HTML, tamaño 400×300 px, incluir ejes y etiquetas.*

---

### Sección D — Control On-Off y Proporcional (20 pts)

#### Problema D.1 — Control de nivel G(s) = 1/(s+1)

**a) Control On-Off con histéresis: ¿se estabiliza?**
No se estabiliza en un valor exacto. El nivel **oscila dentro de la banda de histéresis** (comportamiento de ciclo límite). La bomba enciende cuando el nivel baja del umbral inferior y apaga cuando supera el superior, generando una oscilación sostenida pero acotada. Es aceptable operativamente pero no es un punto de equilibrio.

**b) Control Proporcional Kp=3: ¿llega al setpoint?**
No llega exactamente. Con lazo cerrado:
```
T(s) = 3·G(s)/(1 + 3·G(s)) = 3/(s+1) / (1 + 3/(s+1)) = 3/(s+4)
y_ss = T(0)·1 = 3/4 = 0,75
Offset = 1 - 0,75 = 0,25
```
Existe un **error en estado estacionario (offset) de 25%**. El control proporcional puro siempre deja offset, porque necesita error para generar señal de control.

**c) ¿Qué agregar para eliminar el offset?**
Agregar **acción integral (I)** → controlador **PI o PID**. La integral acumula el error en el tiempo y genera señal de control incluso cuando el error instantáneo es pequeño, eliminando el offset en régimen permanente.

---

#### Problema D.2 — Respuesta con sobrepaso, planta G(s)=1/(s+1)

*(La gráfica muestra respuesta que supera el setpoint y luego se estabiliza en 1 — sin offset, con sobrepaso)*

**a) Tipo de controlador:**
La respuesta llega a 1 (sin offset → hay acción integral) y tiene sobrepaso → **controlador PI o PID**. Más específicamente: sin offset implica al menos integrador (PI); el sobrepaso puede deberse a ganancia alta en PI, o a la acción derivativa de un PID que acelera la respuesta.

**b) ¿Por qué tiene sobrepaso?**
La ganancia proporcional es suficientemente alta como para que el sistema "reaccione con inercia": cuando la salida se acerca al setpoint el error se reduce, pero la señal de control acumulada aún lleva al sistema más allá del objetivo antes de que el integrador revierta la acción.

**c) Si se reduce la ganancia proporcional:**
- El **sobrepaso disminuye** (respuesta más amortiguada)
- El **tiempo de establecimiento aumenta** (respuesta más lenta para llegar al setpoint)
- Hay un trade-off: menos sobrepaso implica mayor tiempo de respuesta.

---

### Sección E — Octave (15 pts)

#### Problema E.1 — Simulación Kp = 2, 5, 10

**Función de transferencia de lazo cerrado:** T(s) = Kp·G/(1+Kp·G) = Kp/(s+1+Kp)

| Kp | Polo LC | y_ss = Kp/(1+Kp) | Offset = 1/(1+Kp) |
|----|---------|-------------------|-------------------|
| 2  | s = -3  | 0,667 (66,7%)     | 0,333 (33,3%)     |
| 5  | s = -6  | 0,833 (83,3%)     | 0,167 (16,7%)     |
| 10 | s = -11 | 0,909 (90,9%)     | 0,091 (9,1%)      |

**Código Octave:**
```octave
pkg load control;
s = tf('s');
G = 1/(s+1);
Kp_vals = [2 5 10];
t = 0:0.01:10;
figure; hold on;
colors = {'b', 'r', 'g'};
for i = 1:length(Kp_vals)
  Kp = Kp_vals(i);
  T = feedback(Kp*G, 1);
  [y, t_out] = step(T, t);
  plot(t_out, y, colors{i}, 'LineWidth', 2, 'DisplayName', sprintf('Kp=%d (offset=%.3f)', Kp, 1-dcgain(T)));
  printf('Kp=%d: y_final=%.4f, offset=%.4f\n', Kp, dcgain(T), 1-dcgain(T));
end
plot(t, ones(size(t)), 'k--', 'LineWidth', 1.5, 'DisplayName', 'Setpoint');
legend('Location', 'southeast');
xlabel('Tiempo (s)'); ylabel('Salida y(t)');
title('Respuesta en lazo cerrado — G(s)=1/(s+1), distintos Kp');
grid on;
```

**c) Resultados numéricos verificados:**
- Kp=2: y_final = 0,6667, offset = 0,3333
- Kp=5: y_final = 0,8333, offset = 0,1667
- Kp=10: y_final = 0,9091, offset = 0,0909

**d) Conclusión:**
A mayor Kp → menor offset. La relación es: **offset = 1/(1+Kp)**. Sin embargo, el offset **nunca es cero** con control proporcional puro, sin importar cuán grande sea Kp. Para eliminar el offset completamente se necesita acción integral (controlador PI o PID). A Kp → ∞ el offset → 0 pero el sistema se vuelve cada vez menos robusto.

---

## Implementación técnica de la página

### Interactividad requerida

1. **B.1c — Gráfico RC:** canvas con dos curvas exponenciales, leyenda, ejes tiempo (0-30s) y tensión (0-5V). Botón "Animar" para dibujar las curvas progresivamente.

2. **C.2d — Mapa de polos:** canvas 400×300 con plano complejo. Ejes, grid, región estable (verde suave), región inestable (rojo suave), puntos en (-1, ±2j) marcados.

3. **E.1 — Simulación Kp:** canvas con las tres curvas de respuesta al escalón (Kp=2, 5, 10) + setpoint. Mostrar tabla con offset calculado. Opcional: slider para Kp variable.

### Footer nav

Agregar en `sistemas-control/teoria.html`, dentro de `.apuntes-footer-nav`:
```html
<a href="ejercicios-parcial.html">📝 Ejercicios Tipo Parcial</a>
```

### Título y hero

```html
<h1>Ejercicios Tipo Parcial</h1>
<p class="subtitle">Sistemas de Control — Ing. Tirabasso</p>
```
Badges/chips: `20 pts · Conceptos` | `25 pts · 1er Orden` | `20 pts · Polos` | `20 pts · Control` | `15 pts · Octave`

---

## Checklist para Desarrollador

- [ ] Crear `sistemas-control/ejercicios-parcial.html`
- [ ] 5 tabs (A–E), CSS inline, color indigo `#3730a3`
- [ ] Canvas para B.1c (curvas RC), C.2d (mapa polos), E.1 (respuesta Kp)
- [ ] Agregar link en footer nav de `teoria.html`
- [ ] Push a GitHub (rama main)
