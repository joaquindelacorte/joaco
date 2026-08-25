# joaco

Sitio personal de Joaquín De La Corte, deployado en [Netlify](https://www.netlify.com/) directo desde este repo (`main`). `index.html` es la landing page; el resto son apuntes de la facultad (cursando Automatización y Control).

## Apuntes por materia

### Análisis Matemático I
- [Teoría 1](analisis-matematico/teoria-1.html) — Funciones, límites, continuidad y curvas de nivel con visualizaciones 3D
- [Teoría 2](analisis-matematico/teoria-2.html) — Versión ampliada: trigonométricas, conjuntos convexos y cheat sheet
- [Teoría 3 — 15 minutos](analisis-matematico/teoria-3.html) — Repaso rápido para el parcial
- [Parcial 2](analisis-matematico/parcial2.html) — Derivadas, integrales, TFC y EDOs, con simuladores y quiz
- [Parcial 2 — Express (20 min)](analisis-matematico/parcial2-express.html) — Fórmulas clave, tablas relámpago, EDOs tipo y mini-quiz
- [Parcial 2 — Modelo](analisis-matematico/parcial2-modelo.html)
- [Parcial 2 — Autoevaluación](analisis-matematico/parcial2-autoevaluacion.html)
- [Regla de la cadena](analisis-matematico/regla-de-la-cadena.html)

### Álgebra Lineal I
- [Teoría](algebra-lineal/teoria.html) — Vectores en R² y R³, producto escalar/vectorial, rectas y planos

### Electrotecnia
- [Teoría](electrotecnia/teoria.html) — Ohm, Kirchhoff, Thévenin/Norton — ejercicios, flashcards y quiz

### Estadística
- [Teoría](estadistica/teoria.html) — *(en blanco, pendiente de contenido)*
- [Parcial 1](estadistica/parcial1.html) — 8 ejercicios resueltos: variables, outliers, probabilidad, binomial
- [Parcial 2](estadistica/parcial2.html) — Binomial y Poisson, simuladores y quiz
- [Resumen](estadistica/resumen.html) — Fórmulas, distribuciones y ejercicios resueltos
- [Repaso 2do Parcial](estadistica/repaso-parcial2.html) — Binomial, Poisson, Normal, intervalos de confianza y regresión lineal
- [Simulacro Parcial 2 — Explicado](estadistica/simulacro-parcial2-explicado.html) — Paso a paso, con juegos interactivos

### Hidráulica
- [Teoría](hidraulica/teoria.html) — Pascal, Bernoulli, Torricelli, Venturi, Reynolds
- [Parcial 2](hidraulica/parcial2.html) — Componentes oleohidráulicos, bombas, válvulas, cavitación y golpe de ariete

### Robótica I
- [Teoría](robotica/teoria.html) — Arduino UNO, entradas, PWM, servomotores e IR

### Sistemas de Control
- [Teoría](sistemas-control/teoria.html) — Apuntes de cátedra clase a clase: lazo abierto/cerrado, modelado matemático, analogías
- [Control PID — Horno](sistemas-control/pid-horno.html) — Proporcional, integral y derivativo, simulador térmico en vivo

### Automatización Industrial
- [Conversión de Bases Numéricas](automatizacion-industrial/conversion-bases.html) — Reglas mnemotécnicas (binario/decimal/hexadecimal) + calculadora interactiva

### Otros
- [LLMs — Cómo piensan](otros/llm.html)
- [Mundial 2026 · Simulador](otros/mundial-2026.html)
- [Prode Mundial 2026 · EV Máximo](otros/prode-mundial-2026.html)

## Estructura

```
index.html              # landing page (linkea a la mayoría de los apuntes de abajo)
netlify.toml            # publish = "." — sirve el repo completo, sin build step
analisis-matematico/
algebra-lineal/
electrotecnia/
estadistica/
hidraulica/
robotica/
sistemas-control/
automatizacion-industrial/
otros/
```
