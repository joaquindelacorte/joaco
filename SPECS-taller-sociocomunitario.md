# SPECS — Taller de Formulación y Desarrollo de Proyectos Sociocomunitarios

## Archivos a crear / modificar

1. **CREAR** `taller-sociocomunitario/teoria.html` — apuntes completos de la materia
2. **MODIFICAR** `index.html` — agregar link en la `notes-grid` de la sección Apuntes

---

## 1. index.html — cambio puntual

En la sección `#apuntes` (línea ~342), dentro del `<div class="notes-grid">`, agregar al final de la lista:

```html
<a class="note-link" href="taller-sociocomunitario/teoria.html">Taller Sociocomunitario</a>
```

---

## 2. taller-sociocomunitario/teoria.html — estructura completa

### Referencia de estilo
Usar como referencia **canónica** `sistemas-control/teoria.html`:
- Mismo sistema de tabs en el nav (una tab por clase)
- Mismo hero con badges-sum
- Mismo sistema de `.page` / `.page.active`
- Mismo CSS inline en `<style>` (no importar estilos externos)
- Colores: usar paleta verde/teal para esta materia — `--main:#0d9488; --main-lt:#14b8a6; --main-bg:#ccfbf1`

### Nav tabs
```
Clase 1 | Clase 2 | Complemento | Clase 3 | Clase 5 | FODA
```

### Hero
```
Título: Taller de Formulación y Desarrollo de Proyectos Sociocomunitarios
Subtítulo: Automatización y Control — UNaP · 2026
Badges: Proyectos · Diagnóstico · Análisis de Causas · FODA · Ishikawa
```

---

## Contenido por tab

### TAB 1 — Clase 1 (14/08/2026): Introducción a los Proyectos

**Sección: ¿Qué es un proyecto?**
Un proyecto es una intervención planificada que transforma una situación problemática o una oportunidad en un resultado concreto.

**Características de los proyectos** (lista):
- Tienen un objetivo definido
- Tienen un inicio y un fin
- Utilizan recursos limitados
- Involucran incertidumbre y riesgos
- Buscan generar un cambio
- Crean un resultado único

**Sección: ¿Por qué hacemos proyectos?**
Los proyectos no son un fin en sí mismos.

Tabla comparativa (2 columnas):
| No hacemos proyectos para… | Hacemos proyectos para… |
|---|---|
| Comprar tecnología | Resolver problemas |
| Instalar sensores | Aprovechar oportunidades |
| Construir algo | Mejorar procesos |
| Implementar un software | Reducir costos / Aumentar seguridad / Generar valor |

**Sección: Problema vs. Solución**

Tabla comparativa:
| Problema | Solución |
|---|---|
| No existe información confiable | Instalar sensores |
| El proceso es lento y manual | Crear una aplicación |
| Existen errores frecuentes | Automatizar una línea |
| La productividad es insuficiente | Comprar equipamiento |

**Callout destacado:** "Antes de diseñar una solución, debemos comprender correctamente el problema que buscamos resolver."

**Sección: ¿De dónde nacen los proyectos?**
Lista: problemas existentes, oportunidades identificadas, necesidades de mejora, cambios tecnológicos, requisitos normativos o legales.

---

### TAB 2 — Clase 2 (21/08/2026): Identificación de Problemas

**Callout principal:**
> Problema = Diferencia entre situación actual y situación deseada.

**Reglas fundamentales** (callout de advertencia):
- No existe proyecto sin problema
- No existe problema sin una situación actual
- No existe proyecto si no sabemos cuál es la situación deseada

**Sección: Tipos de problemas** (lista con iconos o chips):
- Problemas de procesos
- Problemas tecnológicos
- Problemas organizacionales
- Problemas ambientales
- Problemas sociocomunitarios
- Problemas de servicios

**Sección: Herramientas para definir un problema**

Mostrar las 5 herramientas como cards:

**(1) Observación directa**
Relevamiento presencial de la situación en su contexto real.

**(2) Entrevistas y relevamiento**
Fuentes: operadores, vecinos, usuarios, personal de mantenimiento, docentes.

**(3) Recolección de datos**
Ejemplos: tiempos, cantidades, costos, reclamos, frecuencia, indicadores.
⚠️ Nunca trabajar sobre opiniones — buscar evidencia.

**(4) Metodología 5W + 2H**

Tabla:
| Sigla | Pregunta | Qué responde |
|---|---|---|
| What | ¿Qué? | El problema identificado |
| Why | ¿Por qué? | La razón del problema |
| Who | ¿Quién? | Los afectados o responsables |
| Where | ¿Dónde? | El lugar donde ocurre |
| When | ¿Cuándo? | La frecuencia o momento |
| How | ¿Cómo? | La forma en que ocurre |
| How much | ¿Cuánto? | La magnitud o impacto |

**(5) Análisis de Gap**
Comparación sistemática entre la situación actual y la situación deseada. La brecha entre ambas es lo que el proyecto debe cerrar.

---

### TAB 3 — Complemento: Conceptos de Procesos (21/08/2026)

**Sección: Proyecto vs. Proceso**

Tabla comparativa:
| Proyecto | Proceso |
|---|---|
| Temporal, único | Continuo, repetitivo |
| Tiene inicio y fin | Opera de forma permanente |
| Genera un resultado nuevo | Transforma inputs en outputs |
| Involucra incertidumbre | Busca estabilidad y predictibilidad |

**Sección: Propiedades de un proceso**

**Capacidad de Trabajo:** Carga máxima sostenible bajo condiciones especificadas. Los límites vienen de la instalación (hornos, llenadoras, tanques) o las personas. En proceso equilibrado: capacidad = demanda máxima.

**Productividad:** Relación entre recursos entrantes (inputs) y productos salientes (outputs). Se mide como cantidad de producto por unidad de tiempo.

**Sección: Eficacia, Eficiencia y Efectividad** (tabla o 3 cards):

| Concepto | Definición | Pregunta clave |
|---|---|---|
| Eficacia | ¿Cumple el objetivo? | ¿Entregó en tiempo, cantidad y condición? |
| Eficiencia | ¿Aprovecha bien los recursos? | ¿Hay desperdicios (mudas)? |
| Efectividad | ¿Produce lo que el cliente necesita? | ¿Da en el clavo con el problema real? |

Nota: Un proceso puede ser eficaz y eficiente pero inefectivo si el producto no resuelve el problema del cliente.

**Sección: Flexibilidad**
Adaptabilidad ante cambios imprevistos. Incluye velocidad de respuesta y diseño modular que independice etapas críticas.

**Sección: Desperdicios (Mudas)**
Cualquier actividad que consume recursos sin generar valor. Identificarlos y eliminarlos es el objetivo de la mejora continua.
Tipos clásicos (lista): sobreproducción, espera, transporte innecesario, sobreprocesamiento, inventario excesivo, movimientos innecesarios, defectos.

---

### TAB 4 — Clase 3 (28/08/2026): Diagnóstico y Análisis de Contexto

**Callout de definición:**
> "Diagnóstico: forma de ordenar los datos e información sobre cómo es y qué problemas tiene una determinada realidad."

**Diagrama de flujo simple (texto):** Problema → Diagnóstico → Proyecto

**Sección: Recolección de Información**

Dos cards lado a lado:

*Fuentes Primarias* (información obtenida directamente):
- Observación directa
- Entrevistas
- Encuestas
- Relevamientos
- Mediciones

*Fuentes Secundarias* (información generada por otros):
- Informes técnicos
- Normativas
- Estadísticas oficiales
- Artículos académicos
- Estudios previos

Callout: "La combinación de fuentes primarias y secundarias genera diagnósticos más sólidos y confiables."

**Ejemplo real — Plaza sin iluminación:**
Tabla de fuentes usadas en el ejemplo (primarias vs. secundarias), con datos: 75% de vecinos evita la plaza luego de las 20hs / robos aumentaron 18% según Min. de Seguridad.

**Sección: Pensamiento Sistémico**
Un problema rara vez tiene una única causa. Surge de la interacción entre múltiples factores de un mismo sistema. Permite identificar causas y consecuencias más allá de los síntomas visibles.

**Sección: Comprensión Territorial — Mapeo**
Los problemas ocurren dentro de un territorio. El mapeo territorial identifica:
- Recursos disponibles
- Instituciones presentes
- Organizaciones activas
- Relaciones entre actores
- Restricciones y oportunidades

**Sección: Actores Territoriales**

Tabla de 3 columnas:
| Actores Públicos | Actores Privados | Actores Comunitarios |
|---|---|---|
| Municipios | Empresas | ONG |
| Hospitales | Comercios | Cooperativas |
| Escuelas | Cámaras empresariales | Clubes |
| Organismos gubernamentales | — | Asociaciones vecinales, vecinos, usuarios |

**Sección: Interesados (Stakeholders)**
Quienes pueden afectar o ser afectados por el proyecto. Se analizan por:
- **Poder:** capacidad de influir sobre decisiones, recursos o resultados
- **Interés:** grado de involucramiento respecto a la situación

La relación entre ambas variables define estrategias de participación. (Incluir representación visual de la matriz Poder/Interés: 4 cuadrantes con etiquetas Gestionar activamente / Mantener informado / Mantener satisfecho / Monitorear)

**Sección: Factores Endógenos y Exógenos**

Tabla comparativa:
| Factores Endógenos (internos) | Factores Exógenos (externos) |
|---|---|
| Controlables por la organización | Fuera del control directo |
| Recursos humanos, infraestructura, equipamiento | Economía, legislación, políticas públicas |
| Conocimientos técnicos, cultura organizacional | Tendencias tecnológicas, condiciones ambientales |
| Representan **fortalezas y debilidades** | Representan **oportunidades y amenazas** |

**Sección: Herramientas de Análisis**
- **FODA:** integra fortalezas, debilidades, oportunidades y amenazas → usado para diagnóstico
- **PESTEL:** identifica factores exógenos (Político, Económico, Social, Tecnológico, Ecológico, Legal)

---

### TAB 5 — Clase 5 (11/09/2026): Análisis de Problemas y Causas

**Callout de apertura:**
> "Muchas organizaciones actúan sobre los síntomas y no sobre las causas. Las mejoras basadas únicamente en síntomas suelen ser temporales."

**Sección: Síntoma, Problema y Causa**

Diagrama de flujo vertical (con flechas hacia abajo):
```
Causa: Falta de mantenimiento preventivo
        ↓
Problema: Baja disponibilidad de equipos
        ↓
Síntoma: Retrasos en la producción
```

Tabla de tipos de causas:
| Categoría | Ejemplos |
|---|---|
| Técnicas | Equipos, tecnología |
| Organizacionales | Procedimientos, gestión |
| Humanas | Capacitación, habilidades |
| Sociales | Hábitos, comportamientos |
| Económicas | Recursos, financiamiento |
| Regulatorias | Normativa, legislación |

**Sección: Hipótesis**

Callout de definición:
> "Hipótesis: interpretación preliminar que busca responder ¿Qué podría estar generando esta situación?"

Características de una hipótesis (lista con checkmarks):
- Clara y comprensible
- Coherente con la información disponible
- Verificable mediante evidencia
- Específica
- Relacionada directamente con el problema analizado

Ejemplo — Hipótesis vs. Solución:
| ❌ Solución (no es hipótesis) | ✅ Hipótesis |
|---|---|
| "Necesitamos instalar sensores" | "La falta de información en tiempo real podría estar generando errores operativos" |

**Sección: Validación de Hipótesis**
Reunir evidencia para determinar si la explicación propuesta es consistente con la realidad. Usar fuentes primarias y secundarias (ver Clase 2 y Clase 3).

**Sección: Análisis de Causa Raíz — Los 5 Por Qué**
Técnica iterativa: preguntar "¿Por qué?" 5 veces sucesivas hasta llegar a la causa raíz. Evita quedarse en síntomas superficiales. Mostrar ejemplo visual con 5 niveles de pregunta.

**Sección: Diagrama de Ishikawa (Espina de Pescado)**
Organiza visualmente las causas de un problema en categorías. En proyectos sociocomunitarios las categorías se adaptan a dimensiones PESTEL.
Incluir diagrama SVG o representación visual de espina de pescado con 6 ramas etiquetadas (Político, Económico, Social, Tecnológico, Ecológico, Legal) apuntando al problema central.

**Sección: Priorización de Causas — Principio de Pareto**

Criterios de priorización (4 cards):
1. **Impacto** — ¿Qué nivel de influencia tiene sobre el problema?
2. **Frecuencia** — ¿Con qué frecuencia aparece?
3. **Evidencia** — ¿Qué datos respaldan su existencia?
4. **Posibilidad de intervención** — ¿Existe capacidad real para actuar?

Callout Pareto:
> "El principio de Pareto (80/20): aproximadamente el 20% de las causas genera el 80% de los problemas. Concentrar los esfuerzos en las causas de mayor impacto."

**Aplicación al Proyecto Microbasurales — Hipótesis causales:**
- H1: Los microbasurales aparecen porque no existen contenedores cercanos
- H2: Los microbasurales aparecen porque la frecuencia de recolección es insuficiente
- H3: Los microbasurales aparecen por falta de educación ambiental
- H4: Los microbasurales aparecen porque existen terrenos abandonados y sin control

Callout de cierre:
> "Solo cuando las causas han sido identificadas y validadas es posible avanzar: Diseñar y seleccionar soluciones capaces de generar mejoras reales y sostenibles."

---

### TAB 6 — FODA: Análisis del Proyecto Microbasurales

**Header:** "Análisis FODA Preliminar — Proyecto Microbasurales de Pilar"
Subtítulo: "Taller de Formulación y Desarrollo de Proyectos Sociocomunitarios · 2026"

**Layout 2x2 con colores:**
- Fortalezas (verde): metodología estructurada 5W+2H, protocolo de seguridad en campo, privacidad por diseño, bajo costo inicial ($0 licencias), control de calidad con criterios claros
- Debilidades (rojo): roles clave vacantes (Responsable de Datos), presupuesto sin cerrar, punto piloto no consolidado, muestra inicial reducida (1 punto / 2-3 testimonios)
- Oportunidades (azul): respaldo legal Leyes 25.916 y 13.592, predisposición social de vecinos, datos contrastables con fuentes municipales, asistencia académica docente
- Amenazas (amarillo): falta de respuesta municipal, riesgos en territorio (seguridad, clima), retiro de consentimiento vecinal, condicionantes sistémicos (recolección, hábitos, infraestructura)

**Sección: Matriz de Cruce Estratégico**

4 cards con color:
- **FO — Maximizar:** Usar 5W+2H + marco legal para presentar hallazgos al Municipio como reclamo técnico formalizado
- **DO — Compensar:** Aprovechar supervisión docente para validar cuestionarios antes del trabajo de campo
- **FA — Proteger:** Ante posible falta de respuesta municipal, calcular de forma independiente la tasa de reincidencia con observaciones propias
- **DA — Evitar:** Asignar de inmediato un Responsable de Datos para mitigar riesgos de privacidad y asegurar respaldo legal de consentimientos

---

---

## ACTUALIZACIÓN — Desarrollar en profundidad + Quiz

### Instrucción general de desarrollo de contenido

Cada tema debe estar desarrollado en profundidad para que sirva como material de estudio real, no solo como resumen. Usá el siguiente estándar por sección:

- **Explicación extendida:** párrafo(s) que desarrollen el concepto, no solo la definición
- **Por qué importa / Para qué sirve:** contextualizar la utilidad práctica del concepto
- **Ejemplos concretos:** al menos un ejemplo real (puede ser del proyecto Microbasurales u otro contexto de manufactura/sociocomunitario)
- **Errores comunes / Confusiones frecuentes:** advertencias sobre malentendidos típicos
- **Conexión con otros conceptos:** indicar cuándo un concepto se vincula con otra clase

**Temas que necesitan expansión especial:**

**5W+2H:** Ejemplo completo resuelto con el caso Microbasurales en tabla de 7 filas.

**Análisis de Gap:** Diagrama visual (SVG o CSS) con barra Situación Actual vs. Situación Deseada y brecha marcada.

**Pensamiento Sistémico:** Diagrama de ciclo causal: falta de contenedores → acumulación → normalización → más descarte → más acumulación.

**Stakeholders — Matriz Poder/Interés:** Grid visual SVG con 4 cuadrantes y actores reales del proyecto ubicados:
- Alto poder / Alto interés → Municipio de Pilar (Gestionar activamente)
- Alto poder / Bajo interés → Legislatura Provincial (Mantener satisfecho)
- Bajo poder / Alto interés → Vecinos afectados (Mantener informado)
- Bajo poder / Bajo interés → Transeúntes ocasionales (Monitorear)

**Los 5 Por Qué:** Ejemplo completo resuelto para Microbasurales:
1. ¿Por qué hay microbasurales? → Porque la gente tira basura en la calle
2. ¿Por qué tira basura en la calle? → Porque no hay contenedores accesibles
3. ¿Por qué no hay contenedores? → Porque el municipio no los instaló en esas zonas
4. ¿Por qué no los instaló? → Porque no hay relevamiento técnico que justifique la demanda
5. ¿Por qué no hay relevamiento? → Porque no existe un sistema de registro de focos activos → **Causa raíz**

**Diagrama de Ishikawa:** SVG real espina de pescado horizontal con el problema al centro-derecha y 6 ramas PESTEL con causas ejemplo.

**Principio de Pareto:** Gráfico de barras + línea % acumulado (SVG o canvas) con datos de las 4 hipótesis del proyecto.

---

### TAB 7 — Quiz de Validación de Conocimiento

Última tab del nav. **Nav tabs:** `Clase 1 | Clase 2 | Complemento | Clase 3 | Clase 5 | FODA | Quiz`

**Dinámica:**
- Preguntas de opción múltiple (4 opciones, 1 correcta), de a 1 por vez
- Feedback inmediato al responder: verde si correcta / rojo si incorrecta + explicación
- Botón "Siguiente pregunta", barra de progreso "Pregunta X de 30"
- Al finalizar: puntaje total + resumen de errores con respuesta correcta
- Botón "Reiniciar" baraja aleatoriamente (Fisher-Yates shuffle)

**Implementación:** Array JS de objetos `{ pregunta, opciones: ["a)..","b)..","c)..","d).."], correcta: "c", explicacion }`. La propiedad `correcta` indica la letra de la opción correcta — las respuestas ya están mezcladas en posiciones variadas a/b/c/d a lo largo de las 30 preguntas.

---

#### Banco de 30 preguntas — respuestas distribuidas en todas las posiciones

---

##### Clase 1 — Introducción a los Proyectos (5 preguntas)

**P1.** ¿Cuál de las siguientes SÍ es una característica de un proyecto?
- a) Opera de forma continua y repetitiva
- b) Genera siempre el mismo resultado estandarizado
- c) No involucra incertidumbre ni riesgos
- **d) Crea un resultado único ✓**
- Explicación: Los proyectos son únicos e irrepetibles. Continuidad y repetición son propias de los procesos.

**P2.** Un ingeniero propone "implementar un software de gestión". ¿Eso es un proyecto bien formulado?
- a) Sí, tiene un objetivo técnico claro
- **b) No, es una solución — falta identificar el problema que la justifica ✓**
- c) Sí, porque cualquier implementación tecnológica es un proyecto
- d) No, porque no tiene fecha de inicio definida
- Explicación: "Implementar un software" es una respuesta técnica. La pregunta previa siempre debe ser: ¿qué problema concreto resuelve?

**P3.** ¿Por qué hacemos proyectos?
- a) Para adquirir tecnología de última generación
- b) Para cumplir con el presupuesto anual del área
- c) Para construir la infraestructura faltante en una organización
- **d) Para resolver problemas, aprovechar oportunidades y generar valor ✓**
- Explicación: Los proyectos son un medio, no un fin. Comprar tecnología o construir puede ser parte de uno, pero no es el objetivo en sí.

**P4.** ¿Cuál es la principal diferencia entre un proyecto y un proceso?
- **a) El proyecto tiene inicio y fin definidos; el proceso opera de forma continua ✓**
- b) El proceso es siempre más costoso que el proyecto
- c) El proyecto no involucra actores externos al equipo
- d) El proceso genera resultados únicos cada vez
- Explicación: Esta distinción es fundacional. Permite saber cuándo formular un proyecto nuevo vs. cuándo mejorar un proceso existente.

**P5.** ¿De cuáles fuentes pueden nacer proyectos?
- a) Solo de problemas detectados en auditorías internas
- b) Solo de cambios tecnológicos o decisiones regulatorias
- **c) De problemas, oportunidades, necesidades de mejora, cambios tecnológicos o requisitos normativos ✓**
- d) Exclusivamente de decisiones de la alta dirección
- Explicación: Limitar el origen de proyectos a una sola fuente hace perder oportunidades valiosas.

---

##### Clase 2 — Identificación de Problemas (7 preguntas)

**P6.** ¿Cuál es la definición de problema según la materia?
- a) Una situación que genera quejas documentadas de usuarios
- b) Una falla técnica que impide el funcionamiento normal del sistema
- **c) La diferencia entre la situación actual y la situación deseada ✓**
- d) Un conflicto entre actores del territorio
- Explicación: Sin comprender la brecha entre lo actual y lo deseado, no se puede formular un proyecto con sentido.

**P7.** ¿Por qué NO se trabaja sobre opiniones al recolectar datos?
- **a) Porque son subjetivas y no constituyen evidencia verificable ✓**
- b) Porque demoran demasiado el proceso de diagnóstico
- c) Porque no se pueden incluir en informes formales de proyecto
- d) Porque siempre contradicen los datos cuantitativos disponibles
- Explicación: El diagnóstico riguroso requiere datos objetivos: tiempos, frecuencias, costos, indicadores. Las opiniones orientan pero no reemplazan la evidencia.

**P8.** En 5W+2H, ¿qué responde "How much"?
- a) Cómo ocurre el problema paso a paso
- b) Cuántas personas del equipo intervienen en el relevamiento
- c) Qué herramientas se necesitan para resolverlo
- **d) La magnitud o impacto cuantitativo del problema ✓**
- Explicación: Sin cuantificar el impacto, es difícil justificar la inversión en una solución o priorizar frente a otros problemas.

**P9.** Un vecino dice: "siempre hay basura en mi esquina". ¿Es eso un problema bien definido?
- a) Sí, proviene de observación directa (fuente primaria)
- b) Sí, es concreto y ubicado geográficamente
- **c) No, es una percepción — falta cuantificar frecuencia, magnitud y contexto ✓**
- d) No, porque los vecinos no son fuentes metodológicamente válidas
- Explicación: Una percepción es el punto de partida, no el problema. Hay que convertirla en datos: ¿cuántos focos? ¿qué volumen? ¿con qué frecuencia?

**P10.** ¿Qué es el Análisis de Gap?
- a) Una técnica para entrevistar stakeholders clave del proyecto
- **b) La comparación entre situación actual y situación deseada que identifica la brecha a cerrar ✓**
- c) Un diagrama que muestra visualmente las causas del problema
- d) Un análisis de riesgos del entorno externo del proyecto
- Explicación: El gap define el tamaño y la urgencia del proyecto. Cuanto mayor la brecha y menor la tendencia natural a cerrarse, mayor la necesidad de intervención.

**P11.** ¿Cuál de estos es un ejemplo de fuente primaria?
- a) Un informe del INDEC sobre generación de residuos urbanos
- b) Una ordenanza municipal sobre gestión de residuos sólidos
- **c) Una encuesta realizada por el equipo a 40 vecinos del barrio ✓**
- d) Un artículo académico sobre microbasurales en zonas periurbanas
- Explicación: Fuente primaria = generada directamente por quien hace el diagnóstico. Las opciones a, b y d son fuentes secundarias.

**P12.** ¿Cuál es la principal ventaja de combinar fuentes primarias y secundarias?
- a) Reduce significativamente el tiempo de trabajo de campo
- b) Permite prescindir de entrevistas con actores del territorio
- c) Cumple con los requisitos formales de presentación académica
- **d) Genera diagnósticos más sólidos al triangular y corroborar información de múltiples fuentes ✓**
- Explicación: Triangular fuentes reduce sesgos. Si una entrevista y una estadística oficial señalan el mismo problema, la evidencia es mucho más robusta.

---

##### Complemento — Conceptos de Procesos (5 preguntas)

**P13.** ¿Cuál es la diferencia entre eficacia y eficiencia?
- a) Son conceptos equivalentes en gestión de procesos modernos
- **b) La eficacia mide si se cumplió el objetivo; la eficiencia si se usaron bien los recursos ✓**
- c) La eficiencia mide si se cumplió el objetivo; la eficacia si se minimizaron los costos
- d) La eficacia aplica a proyectos y la eficiencia solo a procesos industriales
- Explicación: Regla mnemotécnica: eficAcia → Alcanzar el objetivo. eficiEncia → Economizar recursos.

**P14.** Un proceso produce a tiempo y sin desperdicios, pero el cliente devuelve el producto porque no resuelve su problema. ¿Qué falló?
- **a) La efectividad — el proceso produjo lo incorrecto para el problema real del cliente ✓**
- b) La eficacia — no cumplió el objetivo establecido
- c) La eficiencia — hubo desperdicios no detectados en el proceso
- d) La capacidad — el proceso operó por encima de su límite real
- Explicación: Se puede ser eficaz y eficiente pero inefectivo. La efectividad pregunta: ¿estamos produciendo lo que el cliente realmente necesita?

**P15.** ¿Qué es una "muda"?
- a) Una variación estadística fuera del rango de control del proceso
- b) Una falla técnica registrada en el sistema de gestión de calidad
- c) Un indicador de productividad por debajo del objetivo del período
- **d) Una actividad que consume recursos sin generar valor — un desperdicio ✓**
- Explicación: Las mudas son el blanco principal del Lean/Kaizen. Eliminarlas aumenta la productividad sin agregar recursos.

**P16.** ¿Por qué superar sostenidamente la capacidad de trabajo genera problemas?
- a) Porque el personal rechaza trabajar por encima de ese límite contractual
- b) Porque los costos variables aumentan de forma descontrolada
- **c) Porque la capacidad es el límite físico real del sistema; operarlo por encima genera fallas y degradación ✓**
- d) Porque los indicadores de calidad dejan de ser estadísticamente válidos
- Explicación: La capacidad no es un objetivo ni un promedio: es el techo real del sistema. Ignorarlo de forma sostenida lo rompe.

**P17.** ¿Para qué sirve la flexibilidad en un proceso?
- a) Para reducir los tiempos de ciclo en condiciones normales de operación
- b) Para aumentar la capacidad máxima instalada del proceso
- c) Para garantizar el cumplimiento de auditorías de seguridad e higiene
- **d) Para adaptarse a cambios imprevistos sin detener ni degradar la operación ✓**
- Explicación: Un proceso rígido colapsa ante variaciones de demanda o materia prima. La flexibilidad se diseña con módulos independientes y etapas desacopladas.

---

##### Clase 3 — Diagnóstico y Análisis de Contexto (7 preguntas)

**P18.** ¿En qué etapa del proceso metodológico se ubica el diagnóstico?
- a) Después de diseñar la solución, para validarla con datos
- b) En paralelo con la implementación, para ajustar sobre la marcha
- **c) Entre la identificación del problema y la formulación del proyecto ✓**
- d) Al finalizar el proyecto, para medir el impacto generado
- Explicación: Problema → Diagnóstico → Proyecto. El diagnóstico evita saltar a soluciones sin entender el contexto real.

**P19.** ¿Qué agrega el pensamiento sistémico al diagnóstico?
- **a) Permite ver el problema como parte de un sistema con múltiples causas interrelacionadas ✓**
- b) Acelera la recolección de datos en trabajo de campo
- c) Reduce el número de actores a analizar en el territorio
- d) Identifica al actor responsable principal del problema
- Explicación: El pensamiento sistémico revela retroalimentaciones y cadenas causales que los análisis lineales pasan por alto. Sin él, las soluciones atacan síntomas y el problema reaparece.

**P20.** ¿Cuál de estos actores pertenece a la categoría "comunitario"?
- a) El Municipio de Pilar
- b) Una empresa privada de logística y transporte
- c) El Ministerio de Ambiente de la Provincia de Buenos Aires
- **d) Una asociación vecinal del barrio ✓**
- Explicación: Actores comunitarios: ONG, cooperativas, clubes, asociaciones vecinales, vecinos, usuarios. Municipio y ministerio son públicos; la empresa es privada.

**P21.** Un stakeholder tiene mucho poder pero poco interés en el proyecto. ¿Cuál es la estrategia correcta?
- a) Ignorarlo — si no tiene interés, no va a interferir
- b) Gestionarlo activamente e involucrarlo en todas las decisiones
- c) Incorporarlo al equipo para neutralizar su posible influencia negativa
- **d) Mantenerlo satisfecho para que no use su poder en contra del proyecto ✓**
- Explicación: Alto poder + bajo interés = hay que cuidar la relación. Si se siente ignorado o afectado, puede bloquear el proyecto fácilmente.

**P22.** ¿Cuál de los siguientes es un factor endógeno?
- a) La normativa municipal sobre gestión de residuos sólidos
- b) Las condiciones económicas del municipio en el año electoral
- **c) La experiencia metodológica del equipo de trabajo ✓**
- d) La predisposición de los vecinos del barrio a colaborar
- Explicación: Endógeno = interno, controlable por el equipo. La experiencia del equipo es una fortaleza interna. Los otros ejemplos son factores externos.

**P23.** En el FODA, ¿a qué cuadrante corresponden los factores exógenos?
- a) Solo a las fortalezas, porque son externas al problema
- b) A fortalezas y debilidades, ya que definen la posición competitiva
- **c) A oportunidades y amenazas, ya que son factores del entorno no controlables ✓**
- d) A todos los cuadrantes dependiendo de su naturaleza
- Explicación: Endógeno (controlable) = fortalezas/debilidades. Exógeno (no controlable) = oportunidades/amenazas. Confundirlos lleva a estrategias mal planteadas.

**P24.** ¿Por qué citar la Ley N° 25.916 fortalece el proyecto Microbasurales ante el municipio?
- a) Porque asegura financiamiento directo del Estado Nacional
- b) Porque regula cómo deben registrarse los datos del relevamiento
- **c) Porque convierte el reclamo vecinal en una obligación legal que el municipio debe cumplir ✓**
- d) Porque es una fortaleza interna del equipo (factor endógeno)
- Explicación: La Ley 25.916 exige erradicar focos no autorizados. Citarla transforma una opinión vecinal en un argumento técnico-legal respaldado por norma vigente.

---

##### Clase 5 — Análisis de Problemas y Causas (6 preguntas)

**P25.** En el ejemplo de la materia: los retrasos en producción son ___; la baja disponibilidad de equipos es el ___; la falta de mantenimiento es la ___.
- a) Problema / Causa / Síntoma
- b) Causa / Síntoma / Problema
- **c) Síntoma / Problema / Causa ✓**
- d) Síntoma / Causa / Problema
- Explicación: La cadena siempre va de lo observable hacia lo profundo: síntoma (lo que se ve) → problema (situación no deseada) → causa (lo que lo genera).

**P26.** ¿Cuál afirmación sobre una hipótesis es CORRECTA?
- **a) Es una interpretación preliminar que debe ser verificada con evidencia ✓**
- b) Es una conclusión basada en los datos ya recolectados
- c) Describe la solución más probable al problema identificado
- d) Solo es válida si proviene de un experto en el tema
- Explicación: La hipótesis se construye ANTES de recolectar evidencia. Es provisional y orientadora — guía qué datos buscar, no qué conclusión sacar.

**P27.** ¿Cuál de estas opciones es una hipótesis válida para los microbasurales de Pilar?
- a) "Los vecinos deberían recibir multas por tirar basura en la vía pública"
- b) "Hay que instalar más contenedores en el barrio sur del partido"
- c) "Los habitantes del partido son descuidados con sus residuos"
- **d) "La baja frecuencia de recolección municipal podría estar contribuyendo a la acumulación de residuos" ✓**
- Explicación: a) y b) son soluciones, c) es una opinión subjetiva no verificable. Solo d) cumple: específica, verificable, relacionada al problema, sin juzgar ni proponer solución.

**P28.** Según los "5 Por Qué" del ejemplo, ¿cuál es la causa raíz de los microbasurales?
- a) La gente tira basura porque no hay contenedores cercanos
- b) El municipio no instaló contenedores en esas zonas del partido
- **c) No existe un sistema de registro de focos activos que genere datos para justificar la intervención ✓**
- d) No hay relevamiento técnico que justifique la demanda al municipio
- Explicación: La causa raíz es la última respuesta de la cadena. Las opciones a, b y d son causas intermedias — el "¿por qué?" puede seguir aplicándose.

**P29.** ¿Qué estrategia propone el Principio de Pareto para el análisis de causas?
- a) Eliminar todas las causas identificadas antes de avanzar a la solución
- b) Resolver primero las causas más económicas y rápidas de atacar
- c) Esperar a validar el 100% de las hipótesis antes de tomar acción
- **d) Concentrar esfuerzos en el ~20% de causas que generan el ~80% del problema ✓**
- Explicación: Pareto optimiza recursos limitados. Atacar todo por igual diluye el esfuerzo. Las causas de mayor impacto merecen la mayor atención.

**P30.** ¿Por qué en proyectos sociocomunitarios el Ishikawa usa categorías PESTEL en vez de las 6M industriales?
- a) Porque las 6M son exclusivas de la industria automotriz japonesa
- b) Porque el PESTEL es obligatorio según normativa académica de la UNaP
- **c) Porque las causas en contextos sociocomunitarios son políticas, económicas, sociales y legales, no solo técnicas ✓**
- d) Porque las 6M generan demasiadas ramas y el diagrama se vuelve ilegible
- Explicación: Las 6M (Mano de obra, Máquinas, Materiales, Métodos, Medición, Medio) son para líneas de producción. En proyectos sociocomunitarios las causas clave son legislativas, culturales, económicas y políticas — exactamente lo que captura PESTEL.

---

## Notas técnicas

- **No usar archivos externos de CSS** — todo inline en `<style>` como en `sistemas-control/teoria.html`
- **Mobile-first** — el site es responsivo, respetar patrones existentes
- **Colores de acento:** `--main:#0d9488` (teal) para distinguir esta materia de Sistemas de Control (indigo)
- La página debe funcionar **sin JavaScript del lado del servidor** — solo HTML/CSS/JS vanilla
- El sistema de tabs ya está implementado en las otras páginas, reutilizar ese patrón exacto
- **El quiz debe implementarse en JS vanilla puro** — array de objetos con pregunta/opciones/correcta/explicación, barajado con Fisher-Yates shuffle al iniciar/reiniciar
- **Nav tabs actualizadas:** `Clase 1 | Clase 2 | Complemento | Clase 3 | Clase 5 | FODA | Quiz`
