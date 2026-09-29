# SPECS — IDE Web Octave con Graficación Online

**Archivo a crear:** `sistemas-control/octave-ide.html`
**Repo:** `C:/Users/Joaquin De La Corte/proyectos/joaco/`
**Color:** `--main: #3730a3` (indigo)
**Todo CSS inline en `<style>`, sin externos**

---

## Concepto

IDE web standalone (sin backend, sin servidor) que permite escribir código estilo Octave/MATLAB
para Sistemas de Control, ejecutarlo en el browser y ver los gráficos resultantes en tiempo real.

**No requiere instalar Octave.** Funciona 100% offline una vez cargado.

---

## Stack técnico

| Librería | Uso | Carga |
|----------|-----|-------|
| **CodeMirror 5** (CDN) | Editor con syntax highlight MATLAB/Octave | `<script src="...">` |
| **Plotly.js** (CDN, bundle slim) | Graficación interactiva (zoom, hover, export) | `<script src="...">` |
| **Motor JS propio** | Interpreta el subset de funciones Octave de control | inline en la página |

No usar Pyodide ni WASM (demasiado pesado para este contexto).
No usar backend. Todo corre en el browser.

---

## Layout

```
┌─────────────────────────────────────────────────────┐
│  NAV: 🔬 Octave IDE  [← Teoría] [📝 Parcial]       │
├───────────────────────┬─────────────────────────────┤
│                       │                             │
│   EDITOR              │   GRÁFICOS / OUTPUT         │
│   (CodeMirror)        │   (Plotly.js)               │
│                       │                             │
│   [▶ Ejecutar]        │   [tab: Plot 1 | Plot 2...] │
│   [🗑 Limpiar]        │                             │
├───────────────────────┴─────────────────────────────┤
│   CONSOLA (output de texto / errores)               │
└─────────────────────────────────────────────────────┘
```

**En mobile:** editor arriba, gráfico abajo, consola colapsable.
**Split resizable:** barra central draggable para ajustar ancho editor/gráfico.

---

## Editor

- **CodeMirror 5** con modo `text/x-octave` (o `text/x-matlab` que ya está en CM5)
- Tema dark: `monokai` o `dracula`
- Números de línea, highlight de línea activa, autoindent
- Atajos: `Ctrl+Enter` = ejecutar, `Ctrl+L` = limpiar consola
- Tamaño default: 100% height del panel izquierdo, mínimo 300px
- Font: `JetBrains Mono` o `Fira Code` via Google Fonts CDN, fallback `monospace`

---

## Motor de ejecución JS (funciones Octave implementadas)

El código del usuario se evalúa con `eval()` en un contexto JS enriquecido con estas funciones:

### Variables y operaciones básicas

```javascript
// Asignación normal JS funciona: a = 3, b = [1,2,3]
// Vectores: [1 2 3] → se parsea como array [1,2,3]
// Dos puntos: 0:0.01:10 → linspace equivalente
// Operaciones: +, -, *, /, .*, ./  (element-wise con prefijo punto)
```

Pre-parsear el código antes del eval para convertir sintaxis Octave→JS:
- `0:0.01:10` → `linspace(0,10,1001)` o `range(0,10,0.01)`
- `[1 2 3]` sin comas → `[1,2,3]`
- `%` comentarios → `//`
- `printf(fmt, ...)` → `console_print(fmt, ...)`
- `disp(x)` → `console_print(x)`

### Funciones del motor de control

```javascript
// --- Aritmética de polinomios ---
function linspace(a, b, n)          // vector n puntos de a a b
function zeros(n)                    // array de ceros
function ones(n)                     // array de unos
function polyval(p, x)               // evaluar polinomio en x (array o escalar)
function polyMul(a, b)               // multiplicar polinomios (convolución)
function polyAdd(a, b)               // sumar polinomios
function conv(a, b)                  // alias polyMul (Octave usa conv para polinomios)
function roots(p)                    // raíces del polinomio → array de {re, im}

// --- Objetos de FT ---
function tf(num, den)                // crear objeto FT: {num, den, type:'tf'}
function feedback(G, H=1)            // lazo cerrado: G/(1+G*H), retorna FT
function series(G1, G2)              // en serie: G1*G2, retorna FT
function parallel(G1, G2)            // en paralelo: G1+G2, retorna FT
function pole(G)                     // raíces de den → array {re,im}
function zero(G)                     // raíces de num → array {re,im}
function dcgain(G)                   // G(0) = num(0)/den(0)

// --- Simulación temporal ---
function step(G, t)                  // respuesta al escalón, retorna {t, y}
function impulse(G, t)               // respuesta al impulso
function lsim(G, u, t)               // respuesta a entrada arbitraria u(t)
// Internamente: Euler explícito en espacio de estados, dt=0.005s

// --- Frecuencia ---
function bode(G, w)                  // {mag_db, phase_deg, w} — evalúa G(jω)
function freqs(num, den, w)          // evaluación directa del filtro analógico

// --- Utilidades ---
function abs(x)                      // módulo (escalar o array)
function angle(x)                    // ángulo en rad
function log10(x), log(x), exp(x)   // mat functions en arrays
function max(arr), min(arr)
function length(arr)                 // len del array
function printf(fmt, ...args)        // print formateado a consola
function disp(x)                     // print a consola
```

### Graficación — función `figure` y `plot`

Las llamadas a `figure`, `plot`, `subplot`, `xlabel`, etc. generan gráficos en Plotly:

```javascript
figure()          // crea nueva figura / limpia la actual
hold('on')        // múltiples curvas en la misma figura
hold('off')       // (default)
plot(t, y)        // curva básica
plot(t, y, 'b-')  // con color/estilo tipo Octave: 'r--', 'g-.', 'ko'
plot(t, y, 'b-', 'LineWidth', 2, 'DisplayName', 'y(t)')  // con propiedades
stem(t, y)        // gráfico tipo tallo
xlabel('Texto')
ylabel('Texto')
title('Título')
legend('c1','c2') // o legend('Location','southeast')
grid('on')
xlim([a b])
ylim([a b])
```

Convertir estilo Octave a Plotly:
- `'b-'` → `{color:'blue', dash:'solid'}`
- `'r--'` → `{color:'red', dash:'dash'}`
- `'g-.'` → `{color:'green', dash:'dashdot'}`
- `'ko'` → `{color:'black', mode:'markers', marker:{symbol:'circle'}}`

**Múltiples figuras:** `figure(1)`, `figure(2)` → tabs separados en el panel derecho.

**Función especial `pzmap(G)`:** dibuja mapa de polos/ceros con región LHP/RHP coloreada en Plotly Scatter.

---

## Consola de output

- Fondo oscuro `#1e1e2e`, texto `#cdd6f4`, errores en rojo `#f38ba8`
- Muestra: resultado de `disp()`, `printf()`, valores de variables si se asignan en top-level sin `;`
- En Octave: una expresión sin `;` imprime su resultado → implementar esto
- Botón "🗑 Limpiar consola"

---

## Snippets / ejemplos precargados

Selector dropdown "Cargar ejemplo:" con los casos del curso:

### 1. Sistema de primer orden
```octave
% Sistema de primer orden G(s) = 3/(2s+1)
num = [3];
den = [2 1];
G = tf(num, den);

t = 0:0.01:15;
[y, t_out] = step(G, t);

figure;
plot(t_out, y, 'b-', 'LineWidth', 2, 'DisplayName', 'y(t)');
hold on;
plot(t_out, 3*ones(size(t_out)), 'k--', 'DisplayName', 'y\_ss = 3');
xlabel('Tiempo (s)'); ylabel('Salida');
title('Respuesta al escalón — 1er orden');
legend; grid on;

printf('Valor final: %.4f\n', y(end));
printf('Constante de tiempo τ = %.1f s\n', 2);
```

### 2. Control P — offset
```octave
% Ejercicio E.1 del Parcial: G(s)=1/(s+1), distintos Kp
pkg load control; % ignorado — solo para compatibilidad visual
num = [1]; den = [1 1];
G = tf(num, den);
Kp_vals = [2 5 10];
colors = {'b-', 'r-', 'g-'};
t = 0:0.01:10;

figure; hold on;
for i = 1:length(Kp_vals)
  Kp = Kp_vals(i);
  T = feedback(Kp * G, 1);
  [y, to] = step(T, t);
  oss = 1 - dcgain(T);
  plot(to, y, colors{i}, 'LineWidth', 2, 'DisplayName', sprintf('Kp=%d (offset=%.3f)', Kp, oss));
end
plot(t, ones(size(t)), 'k--', 'LineWidth', 1.5, 'DisplayName', 'Setpoint');
xlabel('Tiempo (s)'); ylabel('y(t)');
title('Control Proporcional — Offset vs Kp');
legend; grid on;
```

### 3. Sistema de segundo orden
```octave
% G(s) = ωn²/(s²+2ζωn·s+ωn²)
wn = 2; zeta = 0.4;
num = [wn^2];
den = [1, 2*zeta*wn, wn^2];
G = tf(num, den);

t = linspace(0, 15, 1500);
[y, to] = step(G, t);

figure;
plot(to, y, 'b-', 'LineWidth', 2);
xlabel('t (s)'); ylabel('y(t)');
title(sprintf('2do orden: ωn=%.1f, ζ=%.2f', wn, zeta));
grid on;

printf('Polos: s = -%.2f ± %.2fj\n', zeta*wn, wn*sqrt(1-zeta^2));
printf('Overshoot ≈ %.1f%%\n', 100*exp(-pi*zeta/sqrt(1-zeta^2)));
```

### 4. Diagrama de Bode
```octave
% Bode de G(s) = 10/(s²+3s+10)
num = [10];
den = [1 3 10];
G = tf(num, den);

w = logspace(-1, 2, 200);
[mag, phase] = bode(G, w);

figure(1);
semilogx(w, mag, 'b-', 'LineWidth', 2);
xlabel('ω (rad/s)'); ylabel('Magnitud (dB)');
title('Bode — Magnitud'); grid on;

figure(2);
semilogx(w, phase, 'r-', 'LineWidth', 2);
xlabel('ω (rad/s)'); ylabel('Fase (°)');
title('Bode — Fase'); grid on;
```

### 5. Mapa de polos y ceros
```octave
% Comparar estabilidad: G1 (estable) vs G2 (inestable)
G1 = tf([1], [1 2]);      % polo en s=-2
G2 = tf([1], [1 -2]);     % polo en s=+2
G3 = tf([1], [1 2 5]);    % polos en s=-1±2j

figure;
pzmap(G1); % marcará × en s=-2
% (mostrar en tabla los polos de cada sistema)
disp('Polos G1:'); disp(pole(G1));
disp('Polos G2:'); disp(pole(G2));
disp('Polos G3:'); disp(pole(G3));
```

---

## Manejo de errores

- Errores de JS (sintaxis, variable no definida) → capturar con try/catch y mostrar en consola en rojo con línea del error
- Si función Octave no está implementada (ej: `rlocus`) → mensaje amigable: `% Función 'rlocus' no implementada aún`
- Línea `pkg load control;` → ignorar silenciosamente (compatibilidad visual)

---

## Navbar y links

Nav propio (hamburger responsive, mismo patrón que teoria.html):
- Brand: "🔬 Octave IDE"
- Tabs: `← Teoría` | `📝 Ejercicios`

Agregar en `teoria.html`:
- Footer nav: `<a href="octave-ide.html">🔬 Octave IDE</a>`
- Tab nav: `<a class="tab-btn" href="octave-ide.html" style="text-decoration:none">🔬 IDE</a>`

---

## Checklist para Desarrollador

- [ ] Crear `sistemas-control/octave-ide.html`
- [ ] Integrar CodeMirror 5 (CDN) con modo MATLAB/Octave + tema dark
- [ ] Integrar Plotly.js (CDN slim)
- [ ] Implementar motor JS: `tf`, `feedback`, `step`, `lsim`, `bode`, `pzmap`, `pole`, `dcgain`, `roots`, `conv`, `linspace`, etc.
- [ ] Pre-parser Octave→JS: `0:h:N`, `[1 2 3]` sin comas, `%` comentarios, `printf`, `disp`
- [ ] Interceptar `plot`, `figure`, `hold`, `xlabel`, `ylabel`, `title`, `legend`, `grid` → Plotly
- [ ] Soporte multi-figura con tabs en panel de gráficos
- [ ] `pzmap` con región LHP/RHP coloreada via Plotly shapes
- [ ] Consola de output: texto + errores con línea
- [ ] 5 snippets precargados en dropdown
- [ ] Layout split: editor izquierda | gráficos derecha | consola abajo
- [ ] Split resizable (drag bar)
- [ ] Responsive mobile: editor arriba, gráfico abajo
- [ ] Ctrl+Enter = ejecutar, Ctrl+L = limpiar consola
- [ ] Agregar links en `teoria.html` (footer nav + tab nav)
- [ ] Push a GitHub rama main
