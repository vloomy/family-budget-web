# Auditoría de PRD — App Móvil de Presupuesto Familiar

_PRD auditado: versión 9 · Fecha de auditoría: 2026-09-16 · Octava iteración (auditoría final de la fase)_

## Veredicto

**Aprobado**

Sin hallazgos Bloqueantes, sin Importantes y **sin Menores**. M-22 está cerrado y no se abre ningún hallazgo nuevo. Es el primer veredicto **Aprobado** del ciclo: los doce ítems del checklist de verificación quedan marcados, algo que no había ocurrido en ninguna de las ocho versiones auditadas.

Acumulado del ciclo completo: **34 hallazgos abiertos, 34 cerrados, 0 vigentes.**

### Sobre el cierre del ciclo

**No hay nada que deba frenar el cierre, y no hay nada que escalar al stakeholder.** Pediste que te lo dijera explícitamente: el PRD versión 9 no tiene hallazgos vigentes de ninguna severidad, así que no existe objeción de auditoría que condicione el handoff al Business Analyst. La decisión de proponerlo es tuya, como lo fue durante todo el ciclo.

Dos aclaraciones para que el veredicto no se lea como más de lo que es:

- **El apartado "No verificable con la información disponible" sigue teniendo cinco entradas, y eso es compatible con un veredicto Aprobado.** No son hallazgos ni pendientes ocultos: son los límites de lo que puedo afirmar sin acceso al brief ni al registro de decisiones del stakeholder. Auditar el PRD es verificar el documento, no validar el negocio que describe.
- **Los cuatro efectos aceptados que el BA hereda siguen vigentes como consecuencias del alcance elegido**, no como defectos: categorías con movimientos en meses cerrados que no podrán eliminarse nunca, pérdida total de datos sin aviso in-app, el tercer dolor del Problema sin validar en esta fase, y criterios de adopción autorreportados. Los cuatro están documentados con causa e impacto en el PRD, que es exactamente donde corresponde que estén.

## Hallazgos

### Bloqueantes

Ninguno.

### Importantes

Ninguno.

### Menores

Ninguno.

### No verificable con la información disponible

Sin cambios respecto de la iteración anterior. Se mantienen como límites declarados de la auditoría, no como pendientes del PRD:

- **Completitud y fidelidad de las resoluciones del stakeholder.** No tengo acceso a `doc/project_brief.md` ni al registro de las decisiones del 2026-09-15 y 2026-09-16. No puedo confirmar que las trece resoluciones incorporadas reflejen lo decidido ni que estén completas. → PM.
- **Conveniencia de la ampliación de alcance de la v6.** Que incorporar categorías personalizables al MVP sea mejor que acotar el mercado o recortar el catálogo es una decisión de negocio. La auditoría verificó que esté trazada y consistente, no que sea la correcta. → Stakeholder.
- **Suficiencia de las muestras** —5 personas para la prueba de comprensión, 10 familias para los criterios de adopción— frente a las decisiones que se tomarán con sus resultados. → Stakeholder.
- **Exactitud de las atribuciones a `project_brief.md`**, incluida la premisa competitiva de §1 y que el brief ubicara las categorías personalizables como post-MVP. Las citas cumplen el requisito del checklist; su contenido no es verificable desde acá. → PM.
- **Aceptabilidad de los cuatro efectos ya asumidos.** Están declarados con claridad y su aceptación es una decisión de negocio ya tomada. → Stakeholder.

## Hallazgo cerrado en la v9

| Hallazgo (v8) | Estado en la v9 |
| --- | --- |
| **M-22 · El riesgo de tensión atribuía cuatro capacidades a la decisión de personalizar** | **Cerrado.** El riesgo cuenta ahora las **tres** capacidades que la decisión efectivamente agregó (crear, renombrar, eliminar) y explica por qué la cuarta no le corresponde: el MVP necesitaba consultar el catálogo incluso con catálogo cerrado, porque registrar un movimiento siempre exigió elegir su categoría, y se declaró por precisión documental. La corrección no solo alinea el conteo con la entrada v8 del Historial: preserva el propósito del riesgo, que es dimensionar el costo real de la decisión de personalizar. Verifiqué las tres referencias numéricas que el párrafo maneja ahora —tres capacidades agregadas, la cuarta capacidad de la sección, y las cuatro decisiones que la capacidad abría, que son los Puntos Abiertos 10 a 13— y las tres son correctas y designan cosas distintas. |

## Verificación final del documento

Al ser la auditoría de cierre, revisé el documento completo y no solo el párrafo modificado.

**Referencias cruzadas** — verificadas todas, ninguna rota:

| Referencia desde | Apunta a | Correcto |
| --- | --- | --- |
| Alcance — No incluye (acceso del usuario a meses anteriores) | Ítem 7 · Eliminar una categoría | Sí |
| Supuestos · Mercado objetivo | Ítems 5 a 7 · Crear, renombrar, eliminar | Sí |
| Supuestos · Categorías | Ítem 7, como fuente única de la regla de eliminación | Sí |
| Riesgo de tensión por personalización | Dolores 1 y 2 del Problema | Sí |
| Riesgo de dolor familiar no validado | Tercer dolor del Problema | Sí |
| Historial · entradas v6 y v7 | Ítems según la numeración vigente en su momento | Sí, bajo la convención declarada en la entrada v8 |
| Historial · entrada v8 | Ítems 4 a 7 en la numeración actual | Sí |

**Consistencia interna** — verificada en los puntos que el ciclo mostró como más frágiles:

- Los conteos de ítems de Alcance — Incluye a lo largo del Historial son aritméticamente consistentes: 10 → 7 (v2), 6 (v3), 7 (v5), 8 (v6), 10 (v7), 11 (v8), sin cambios en la v9.
- El catálogo enumera 10 categorías de gasto y 3 de ingreso, coincidente con el total de 13 declarado, y cada tipo determina en qué total del resumen participa.
- La regla de eliminación de categorías está declarada en un solo lugar —ítem 7— y las otras dos secciones que la necesitan remiten a él en vez de reformularla.
- Los cuatro Criterios de éxito tienen umbral y método, con la unidad de medición declarada y la ventana de seguimiento derivada del propio criterio D30.
- Las entradas v2, v3 y v4 del Historial, restauradas en la v7, siguen íntegras: dos versiones consecutivas sin volver a condensarlas confirman que el cambio de método —ediciones puntuales en lugar de reescritura completa— sostuvo el resultado.

**Regresiones** — ninguna. Los 33 hallazgos cerrados en iteraciones anteriores siguen resueltos. Verifiqué en particular que la corrección de la v9, al reescribir un párrafo de Riesgos, no reintrodujera una formulación prescriptiva que sumara alcance por fuera de Alcance — Incluye, que fue el defecto original de I-5 y el que más veces estuvo en riesgo de volver: el párrafo describe causa, impacto y mitigación ejecutada, sin prescribir capacidades.

## Checklist de verificación

Aplicado sobre la versión 9. **Los doce ítems quedan marcados, por primera vez en el ciclo.**

- [x] Metadata (versión/fecha) presente y consistente con el Historial de Cambios del PRD. — Versión 9 / 2026-09-16, con nueve entradas, decisiones fechadas y atribuidas, y la entrada v9 identificando su único cambio y el veredicto que lo originó.
- [x] Problema describe un dolor concreto y verificable, no una solución disfrazada de problema. — Tres dolores numerados como situación actual, con insumo citado, y con la delimitación explícita de cuáles ataca el MVP y cuál queda diferido.
- [x] Objetivo es distinto del Problema, y expresa un resultado de negocio mensurable. — Distinto del Problema, enunciado sobre el actor confirmado del MVP y respaldado por cuatro criterios verificables.
- [x] Todos los actores usados en Alcance, Reglas o Criterios están definidos en Actores. — El perfil único cubre las capacidades declaradas, incluida la gestión de categorías; los actores de fases posteriores están definidos y marcados como fuera del MVP; la equivalencia entre familia participante y usuario/dispositivo está declarada en el método de verificación.
- [x] Cada ítem de Alcance — Incluye es una unidad acotada y clara (candidata razonable a 1 HU), sin combinarse ni superponerse con otros ítems. — Los 11 ítems son capacidades acotadas y distintas, con las cuatro de categorías separadas por tener reglas propias y el ítem de presupuesto declarado explícitamente como una sola capacidad.
- [x] Alcance — No incluye es específico (no genérico ni vacío) y delimita casos ambiguos o adyacentes reales. — 15 exclusiones concretas, con la de meses anteriores acotada al plano del usuario y con la referencia correcta al ítem que exige la verificación interna.
- [x] Supuestos y Restricciones contiene solo datos confirmados — nada que en realidad sea incierto y debería estar en Puntos Abiertos. — Las once entradas están confirmadas, el encabezado no anuncia salvedades inexistentes y la regla compartida remite a su fuente única.
- [x] Riesgos y Dependencias (si la sección existe) tiene causa e impacto identificables, no está redactada en términos vagos. — Dependencias declaradas como inexistentes con justificación; los seis riesgos identifican causa e impacto, y el de tensión por personalización ya dimensiona correctamente lo que la decisión agregó.
- [x] Criterios de éxito son medibles/verificables y están alineados con el Objetivo. — Los cuatro tienen umbral y método de verificación, alineados con el doble objetivo de constancia de registro y visibilidad del presupuesto.
- [x] Cada Punto Abierto tiene la pregunta exacta a resolver y el destinatario (a quién se le preguntaría). — No hay puntos vigentes. La sección existe y declara explícitamente esa condición, y las trece resoluciones fueron verificadas en secciones normativas.
- [x] No hay contradicciones entre Alcance — Incluye y Alcance — No incluye. — Verificado ítem por ítem, incluida la única frontera que requiere lectura fina: eliminar una categoría exige evaluar meses anteriores que el usuario no puede consultar, distinción resuelta en el texto de la propia exclusión.
- [x] No hay afirmaciones que se lean como hechos de negocio decididos sin respaldo en Supuestos y Restricciones ni en un insumo citado. — Las decisiones están atribuidas al stakeholder con fecha, la reversión de la exclusión del brief está declarada como tal, y la premisa competitiva sigue atribuida y calificada como premisa.

## Cierre del ciclo de auditoría

Ocho iteraciones sobre nueve versiones del PRD (la v6 no se auditó como versión, por decisión del PM). **34 hallazgos abiertos y 34 cerrados**, sin ninguno vigente y sin regresiones en todo el ciclo.

Trazo el recorrido porque es lo que sostiene el veredicto final:

| Iteración | Versión | Veredicto | B · I · M |
| --- | --- | --- | --- |
| 1.ª | 1 | Aprobado con observaciones | 0 · 6 · 6 |
| 2.ª | 2 | Aprobado con observaciones | 0 · 3 · 3 |
| 3.ª | 3 | Aprobado con observaciones | 0 · 1 · 3 |
| 4.ª | 4 | Aprobado con observaciones | 0 · 1 · 0 |
| 5.ª | 5 | Aprobado con observaciones | 0 · 2 · 4 |
| 6.ª | 7 | Aprobado con observaciones | 0 · 1 · 5 |
| 7.ª | 8 | Aprobado con observaciones | 0 · 0 · 1 |
| 8.ª | 9 | **Aprobado** | 0 · 0 · 0 |

Dos hallazgos merecen quedar registrados como los de mayor consecuencia del ciclo, porque no fueron correcciones de forma:

- **I-9** estuvo vigente cuatro iteraciones y no se cerró por redacción: el PRD no tenía ningún criterio con el que declarar éxito o fracaso, y solo se cerró cuando el stakeholder definió umbrales y método. Sostenerlo abierto sin que bloqueara el avance fue lo que evitó que el MVP arrancara sin criterios de aceptación de negocio.
- **I-10** derivó en el primer y único cambio de alcance del proyecto: la contradicción entre un catálogo cerrado con categorías específicas y un mercado objetivo de "cualquier familia" se resolvió habilitando la personalización, decisión del stakeholder que revirtió una exclusión del brief y quedó declarada como cambio de alcance en vez de disimularse como corrección.

**Definition of Done del rol, verificada:** existe este documento con veredicto explícito y versión auditada identificada; todos los hallazgos Bloqueantes e Importantes del ciclo indicaron sección afectada, descripción y corrección sugerida; el checklist está completo en las ocho iteraciones; el Historial de Auditorías refleja todas las iteraciones; y no hay contenido de negocio inventado por la auditoría — lo no verificable quedó siempre declarado como tal.

El ciclo queda cerrado desde la auditoría. Si el PRD se modifica después del handoff, corresponde una nueva iteración sobre la versión resultante.

## Historial de Auditorías

- 2026-09-15 — versión auditada 1 — Aprobado con observaciones (0 Bloqueantes · 6 Importantes · 6 Menores).
- 2026-09-15 — versión auditada 2 — Aprobado con observaciones (0 Bloqueantes · 3 Importantes · 3 Menores). Los 12 hallazgos de la v1 verificados como resueltos; 6 hallazgos nuevos, sin regresiones.
- 2026-09-15 — versión auditada 3 — Aprobado con observaciones (0 Bloqueantes · 1 Importante · 3 Menores). Cinco de los 6 hallazgos de la v2 cerrados; I-9 vigente. Renumeración de Puntos Abiertos verificada sin referencias cruzadas rotas.
- 2026-09-15 — versión auditada 4 — Aprobado con observaciones (0 Bloqueantes · 1 Importante vigente · 0 Menores). Los 3 Menores de la v3 cerrados; sin hallazgos nuevos y sin regresiones.
- 2026-09-16 — versión auditada 5 — Aprobado con observaciones (0 Bloqueantes · 2 Importantes · 4 Menores). Los 9 Puntos Abiertos cerrados y verificados en secciones normativas; **I-9 cerrado** tras cuatro iteraciones vigente.
- 2026-09-16 — versión auditada 7 — Aprobado con observaciones (0 Bloqueantes · 1 Importante · 5 Menores). La v6 no se auditó como versión, por decisión del PM. Los 6 hallazgos de la v5 cerrados, incluidos I-10 e I-11. Primera ampliación de alcance del proyecto, verificada como trazada y consistente.
- 2026-09-16 — versión auditada 8 — Aprobado con observaciones (0 Bloqueantes · 0 Importantes · 1 Menor). Los 6 hallazgos de la v7 cerrados, incluido I-12. Renumeración de Alcance — Incluye verificada sin referencias cruzadas rotas.
- 2026-09-16 — versión auditada 9 — **Aprobado** (0 Bloqueantes · 0 Importantes · 0 Menores). M-22 cerrado, sin hallazgos nuevos y sin regresiones. Los doce ítems del checklist marcados por primera vez en el ciclo. Acumulado: 34 hallazgos abiertos, 34 cerrados, 0 vigentes. Nada impide el cierre del ciclo ni el handoff al BA; la decisión es del PM.
