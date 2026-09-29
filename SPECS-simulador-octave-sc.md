# SPECS — Simulador Octave / Control — Sistemas de Control

**Archivo a crear:** `sistemas-control/simulador-octave.html`
**Repo:** `C:/Users/Joaquin De La Corte/proyectos/joaco/`
**Color:** `--main: #3730a3` (indigo, igual que teoria.html)
**Referencia de estilo base:** `sistemas-control/pid-horno.html` — sliders, canvas, layout responsivo
**Todo CSS inline en `<style>`, sin externos**

---

## Objetivo

Página standalone que replica lo que un estudiante haría en Octave para Sistemas de Control:
ingresa una función de transferencia (numerador/denominador), elige tipo de entrada (escalón, rampa, senoidal) y ve la respuesta graficada en tiempo real — sin correr Octave.

Además muestra el **código Octave equivalente** generado automáticamente para que el alumno lo pueda copiar y ejecutar.

---

## Secciones (tabs)

```
📐 Respuesta Temporal | 📊 Diagrama de Bode | 🗺️ Mapa de Polos/Ceros | 💻 Código Octave
```

IDs: `page-resp`, `page-bode`, `page-pzmap`, `page-octave`

---

## Sección 1 — Respuesta Temporal

### Panel de configuración (izquierda / arriba en mobile)

**Función de transferencia — ingreso por coeficientes:**
```
Numerador:    [input text]  ej: "3" o "1 2" (coefs de mayor a menor grado)
Denominador:  [input text]  ej: "2 1" o "1 3 2"
```
→ Parsear como arrays de coeficientes. Ej: "1 3 2" → [1, 3, 2] → s² + 3s + 2

**Tipo de entrada:**
- Radio buttons: Escalón unitario | Escalón (amplitud) | Rampa | Senoidal
- Si Escalón amplitud: slider/input 0.1–10, default 1
- Si Senoidal: slider frecuencia 0.1–10 rad/s, amplitud 1–5

**Tiempo de simulación:** slider 1–30 s, default 10 s

**Controlador (opcional):**
- Checkbox "Agregar controlador"
- Si activo: select Proporcional / PI / PID
  - Kp: slider 0.1–20, default 1
  - Ki (PI/PID): slider 0–5, default 0
  - Kd (PID): slider 0–5, default 0
- Selector: Lazo Abierto | Lazo Cerrado (feedback unitario)

**Botón:** `▶ Simular`  (también recalcula automático al cambiar sliders)

### Canvas principal — Respuesta temporal

- Tamaño: full-width, height 280px (desktop) / 220px (mobile)
- Eje X: Tiempo (s), eje Y: Amplitud
- Curva de salida y(t): color indigo `#6366f1`
- Línea de setpoint punteada: gris `#9ca3af`
- Si hay controlador PI/PID: mostrar también la señal de control u(t) en naranja `#f97316` (checkbox para mostrar/ocultar)
- Grid suave, ejes con labels, tooltip al hover mostrando (t, y)

### Métricas calculadas (debajo del gráfico)

Mostrar en chips/cards:
- **y_ss** — valor final (estado estacionario)
- **Offset** — si setpoint=1: `1 - y_ss`
- **t_rise** — tiempo de subida (10% → 90% del valor final)
- **t_settle** — tiempo de establecimiento (±2% del valor final)
- **Overshoot %** — si hay sobrepaso: `(y_max - y_ss) / y_ss × 100`
- **Polos** — lista de polos de la FT (o del sistema en lazo cerrado si aplica)

### Algoritmo de simulación

Usar **método de Euler explícito** en espacio de estados para la respuesta temporal.
Para FT G(s) = N(s)/D(s), convertir a forma canónica controlable:

```javascript
// Dado num = [b0, b1, ...bm] y den = [a0, a1, ...an] (grado n > m)
// Normalizar: dividir todo por a0
// Matrices A (companion), B, C, D estándar

function tf2ss(num, den) {
  // Normalizar den
  const a0 = den[0];
  const a = den.map(x => x/a0);
  const b = num.map(x => x/a0);
  const n = a.length - 1; // orden
  // Matriz A companion form
  // A = [[0,1,0,...], [0,0,1,...], ..., [-a[n], -a[n-1], ..., -a[1]]]
  // B = [0, 0, ..., 1]^T
  // C y D dependen de los coeficientes del numerador (forma observable)
  // Retornar {A, B, C, D}
}

function simulateEuler(A, B, C, D, u_fn, t_end, dt=0.01) {
  // x[k+1] = x[k] + dt*(A*x[k] + B*u[k])
  // y[k] = C*x[k] + D*u[k]
  // Retornar arrays {t, y, u}
}
```

dt = 0.005s (suficiente para sistemas hasta ~10 rad/s). Si el sistema es de orden 1 o 2, resolver analíticamente para mayor precisión.

**Para lazo cerrado con controlador:**
Calcular la FT de lazo cerrado T(s) = C(s)·G(s) / (1 + C(s)·G(s)) multiplicando polinomios, luego simular T(s).

**Multiplicación de polinomios:** convolución de coeficientes (función `polyMul`).
**Suma de polinomios:** alinear por grado y sumar (función `polyAdd`).

---

## Sección 2 — Diagrama de Bode

### Gráficos

Dos canvas apilados:
1. **Magnitud** (dB) vs frecuencia (rad/s) — height 200px
2. **Fase** (°) vs frecuencia (rad/s) — height 180px

- Eje X: escala logarítmica, 0.01 a 1000 rad/s
- Grid en décadas, etiquetas: 0.01, 0.1, 1, 10, 100, 1000
- Línea de magnitud: indigo
- Línea de fase: naranja
- Margen de ganancia y margen de fase marcados con líneas verticales punteadas + etiqueta numérica

### Cálculo

```javascript
// Para cada ω: evaluar G(jω)
// H(jω) = N(jω) / D(jω)
// Numerador/denominador son polinomios evaluados en s = jω
// |H| en dB = 20*log10(|H(jω)|)
// fase = atan2(Im, Re) en grados

function evalPoly(coeffs, jw) {
  // coeffs [a0, a1, ..., an] → a0*s^n + a1*s^(n-1) + ... + an
  // s = jω → s^k = (jω)^k usando potencias de números complejos
  // Retornar {re, im}
}
```

Rango de frecuencias: 200 puntos logarítmicamente espaciados entre 0.01 y 1000 rad/s.

### Métricas de Bode

- **Frecuencia de corte (ωc):** donde |H(jω)| = 0 dB
- **Margen de fase (PM):** 180° + ∠H(jωc)
- **Frecuencia de cruce de fase (ωp):** donde ∠H(jω) = -180°
- **Margen de ganancia (GM):** -20·log10(|H(jωp)|) en dB

Mostrar en chips debajo del gráfico.

---

## Sección 3 — Mapa de Polos y Ceros

### Canvas

- Tamaño: 500×380px centrado (o full-width en mobile)
- Plano complejo: eje real (horizontal), eje imaginario (vertical)
- Región LHP (parte real < 0): fondo verde muy suave `rgba(34,197,94,0.06)`
- Región RHP (parte real > 0): fondo rojo muy suave `rgba(239,68,68,0.06)`
- Grid gris suave, ejes con labels
- **Polos:** marcados con × rojo, tamaño 12px, tooltip con valor exacto
- **Ceros:** marcados con ○ azul (borde indigo), tooltip con valor exacto
- Si hay controlador en LC: mostrar polos de LC con color diferente (naranja) y leyenda

### Cálculo de polos/ceros

```javascript
// Polos: raíces del denominador
// Ceros: raíces del numerador
// Usar companion matrix + eigenvalues (método numérico)
// O para orden ≤ 2: fórmula analítica
// Para orden 3+: método de Durand-Kerner o Newton-Horner iterativo

function polyRoots(coeffs) {
  const n = coeffs.length - 1;
  if (n === 1) return [{ re: -coeffs[1]/coeffs[0], im: 0 }];
  if (n === 2) {
    // fórmula cuadrática → retornar raíces complejas
  }
  // n ≥ 3: Durand-Kerner
}
```

### Panel lateral

- Tabla con polos: columna `s = σ ± jω`, columna `Estable` (✅/❌), columna `Tipo` (real/complejo)
- Indicador general: "Sistema ESTABLE" (todos polos LHP) o "INESTABLE" (algún polo RHP/eje imaginario)

---

## Sección 4 — Código Octave

### Panel de código generado

Textarea/pre con syntax highlight simple (comentarios en verde, keywords en azul) mostrando el código Octave equivalente a la configuración actual.

Template generado dinámicamente:

```octave
% === Simulación generada por Simulador Octave — joacodelacorte.netlify.app ===
pkg load control;

% Función de transferencia
num = [<NUM>];
den = [<DEN>];
G = tf(num, den);

% Controlador
<CONTROLLER_BLOCK>

% Respuesta al escalón
t = 0:0.01:<T_END>;
[y, t_out] = step(<SYS>, t);

% Graficar
figure;
plot(t_out, y, 'b-', 'LineWidth', 2);
hold on;
plot(t_out, ones(size(t_out)), 'k--', 'LineWidth', 1.5);
xlabel('Tiempo (s)'); ylabel('Salida y(t)');
title('Respuesta al escalón');
legend('y(t)', 'Setpoint');
grid on;

% Métricas
printf('Valor final: %.4f\n', y(end));
printf('Offset: %.4f\n', 1 - y(end));
```

**Si entrada es senoidal:**
```octave
u = <AMP>*sin(<FREQ>*t);
y = lsim(<SYS>, u, t);
plot(t, y, t, u);
```

**Botón "📋 Copiar código"** — copia al portapapeles con `navigator.clipboard.writeText()`

### Sub-sección: Referencia rápida de comandos

Tabla de 2 columnas: Función Octave | Descripción
- `tf(num, den)` → crear FT
- `feedback(G, H)` → lazo cerrado
- `step(G, t)` → respuesta al escalón
- `bode(G)` → diagrama de Bode
- `pzmap(G)` → mapa polos/ceros
- `pole(G)` → calcular polos
- `dcgain(G)` → ganancia DC (estado estacionario)
- `lsim(G, u, t)` → respuesta a entrada arbitraria

---

## Casos de prueba precargados (selector)

Dropdown "Cargar ejemplo:" con:

| Nombre | Num | Den | Controlador |
|--------|-----|-----|-------------|
| Primer orden simple | `[3]` | `[2,1]` | — |
| Segundo orden subamortiguado | `[1]` | `[1,0.4,4]` | — |
| Integrador puro | `[1]` | `[1,0]` | — |
| Control P con offset | `[1]` | `[1,1]` | P, Kp=2, LC |
| Control PI sin offset | `[1]` | `[1,1]` | PI, Kp=2, Ki=1, LC |
| Ejercicio E.1 (Parcial) | `[1]` | `[1,1]` | P, Kp=2/5/10, LC |

Para "Ejercicio E.1": botones rápidos `Kp=2`, `Kp=5`, `Kp=10` que actualizan el slider y resimulan.

---

## Links y navegación

**Nav propio (mismo patrón hamburger de teoria.html):**
- Brand: "🔬 Simulador Octave"
- Links: `← Volver a Teoría` (href: teoria.html) | `📝 Ejercicios Parcial` (href: ejercicios-parcial.html)

**Agregar en `teoria.html` footer nav:**
```html
<a href="simulador-octave.html">🔬 Simulador Octave</a>
```

**Agregar en `teoria.html` nav tabs (al lado de Simuladores):**
```html
<a class="tab-btn" href="simulador-octave.html" style="text-decoration:none">🔬 Octave</a>
```

---

## Checklist para Desarrollador

- [ ] Crear `sistemas-control/simulador-octave.html`
- [ ] CSS inline, color `--main:#3730a3`, misma tipografía/tokens que teoria.html
- [ ] Sección 1: inputs FT + sliders controlador + canvas respuesta temporal + métricas
- [ ] Algoritmo Euler en espacio de estados para FT arbitraria de orden 1-4
- [ ] Sección 2: canvas Bode (magnitud + fase) con márgenes calculados
- [ ] Sección 3: canvas mapa polos/ceros con región estable/inestable coloreada
- [ ] Sección 4: código Octave generado dinámicamente + botón copiar + tabla referencia
- [ ] Dropdown con 6 casos precargados + botones Kp=2/5/10 para E.1
- [ ] Nav hamburger responsive (misma lógica que teoria.html)
- [ ] Agregar link en `teoria.html`: footer nav + tab en nav principal
- [ ] Push a GitHub rama main
