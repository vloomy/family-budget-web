# PRD — App Móvil de Presupuesto Familiar

_Versión: 10 · Última actualización: 2026-09-17_

> Fuente de insumos: `doc/project_brief.md` (brief de stakeholder) más las decisiones del stakeholder del 2026-09-15 y 2026-09-16. Toda afirmación de negocio de este PRD proviene de esas fuentes.

## Problema

Las familias gestionan su dinero de forma informal: anotaciones sueltas, mensajes de chat, planillas dispersas o solo "de memoria" (`project_brief.md` §1). Esa informalidad produce hoy tres situaciones concretas:

1. El registro de ingresos y gastos del día a día se abandona o queda incompleto, porque anotarlo donde sea implica fricción.
2. Nadie sabe cuánto queda disponible por categoría (comida, servicios, gasolina, etc.), así que el exceso se descubre después de haberlo gastado.
3. Los miembros de la familia no logran ponerse de acuerdo sobre en qué se gasta, porque no comparten una misma fuente de información.

El MVP ataca los dolores 1 y 2. El dolor 3 **queda diferido a la fase de multiusuario**: por decisión del stakeholder (2026-09-15), el uso compartido del hogar recién se valida cuando exista presupuesto compartido entre varios miembros, que está fuera de este alcance.

Según el brief (`project_brief.md` §1), las apps de finanzas existentes no resuelven esto porque suelen ser complejas, orientadas a un solo usuario o cargadas de funciones que una familia promedio no necesita. Es una premisa del stakeholder, no un benchmark verificado por el equipo.

## Objetivo

Que el usuario del hogar pueda **entender y controlar el dinero mensual de la familia desde la app**, reemplazando planillas y anotaciones informales por una única herramienta simple y clara.

La mejora concreta que persigue el MVP es doble: que el usuario **registre los movimientos con constancia** (hoy no ocurre, o se hace de forma dispersa) y que **sepa en todo momento cómo va el presupuesto del mes** sin tener que calcularlo ni reconstruirlo.

El objetivo de producto de fases posteriores —que la familia completa gestione el presupuesto de forma compartida y logre acordar en qué se gasta— depende del multiusuario, fuera del MVP.

## Actores

Para el MVP se confirmó un **único perfil de usuario sin distinción de roles**, en un solo dispositivo y sin cuentas:

- **Usuario del hogar (único perfil del MVP):** registra gastos e ingresos, gestiona sus categorías, define el presupuesto mensual por categoría y consulta el estado del mes. Público general, no experto en finanzas, hispanohablante.

Actores previstos para fases posteriores (no aplican al MVP; se documentan para que la arquitectura no los bloquee):

- **Miembro de la familia:** registra movimientos y consulta el presupuesto compartido.
- **Administrador del hogar:** además de lo anterior, define el presupuesto por categoría y gestiona quién forma parte del grupo familiar.

## Alcance — Incluye

Capacidades de producto observables por el usuario que componen el MVP. Las condiciones transversales (plataforma, moneda, persistencia local, idioma, ausencia de cuentas, catálogo inicial de categorías) no se listan aquí: son restricciones y viven en Supuestos y Restricciones.

1. **Registrar un movimiento** (gasto o ingreso) con monto, fecha, categoría y nota opcional.
2. **Definir el presupuesto mensual de una categoría**, sea del catálogo inicial o creada por el usuario. Es una sola capacidad: fijar el monto de una categoría que no lo tiene y ajustar el de una que ya lo tiene son el mismo flujo, sin reglas diferenciadas.
3. **Arrastre automático del presupuesto al mes siguiente:** al iniciar un nuevo mes, los montos presupuestados del mes anterior se mantienen sin que el usuario los redefina. El **saldo no gastado no se acumula**: el presupuesto del nuevo mes parte del mismo monto, no del monto más el sobrante.
4. **Consultar el catálogo de categorías** vigente, con su tipo (gasto o ingreso), incluidas las creadas por el usuario y las que no tienen presupuesto ni movimientos en el mes.
5. **Crear una categoría propia**, declarando al crearla si es de gasto o de ingreso. El tipo determina en qué total del resumen participan sus movimientos.
6. **Renombrar una categoría**, propia o del catálogo inicial.
7. **Eliminar una categoría**, propia o del catálogo inicial, **solo si no tiene movimientos registrados en ningún mes**. Mientras los tenga, la eliminación se impide; el usuario puede renombrarla.
8. **Consultar el resumen del mes en curso:** total ingresado, total gastado, saldo disponible y avance por categoría (gastado vs. presupuestado), incluidas las categorías creadas por el usuario.
9. **Consultar el listado de movimientos del mes en curso.**
10. **Editar un movimiento del mes en curso.**
11. **Eliminar un movimiento del mes en curso.**

## Alcance — No incluye (por ahora)

Todo lo siguiente queda explícitamente fuera del MVP y es candidato a fases posteriores, a priorizar una vez validado el MVP:

- **Sincronización y multiusuario:** varios miembros de la familia compartiendo el mismo presupuesto en tiempo real (requiere cuentas y backend).
- **Cuentas, registro y login.**
- **Roles diferenciados** (administrador del hogar vs. miembro) y gestión de integrantes del grupo familiar.
- **Acceso del usuario a movimientos de meses anteriores**: consultarlos, editarlos o eliminarlos. El MVP opera sobre el mes en curso. La exclusión aplica a lo que el usuario puede hacer, no impide las verificaciones internas que requieren las reglas declaradas —por ejemplo, comprobar si una categoría tiene movimientos en algún mes antes de permitir eliminarla (ítem 7 de Alcance — Incluye).
- **Acumulación del saldo no gastado** entre meses: el sobrante de una categoría se descarta al cerrar el mes.
- **Reportes históricos y gráficos** de tendencias entre meses.
- **Gastos recurrentes** y recordatorios (alquiler, servicios, suscripciones).
- **Alertas** al acercarse o superar el presupuesto de una categoría.
- **Metas de ahorro.**
- **Exportar datos** (CSV / PDF).
- **Múltiples monedas** y soporte multi-idioma.
- **Adjuntar foto de comprobante** a un movimiento.
- **Respaldo o restauración de datos.**
- **Aviso in-app sobre la ausencia de respaldo:** el usuario no será advertido de que sus datos son locales y no se respaldan (decisión del stakeholder, 2026-09-15).
- **Analítica o telemetría de uso**, incluso anónima. Los criterios de adopción se validan por entrevistas y pruebas con usuarios, no por instrumentación del producto.

## Supuestos y Restricciones

Datos confirmados por el stakeholder que acotan el proyecto:

- **Plataforma:** producto móvil multiplataforma (iOS y Android), una sola base de código.
- **Complejidad:** baja por diseño. Ante cualquier disyuntiva, se prioriza la simplicidad sobre la cantidad de funciones.
- **Persistencia:** almacenamiento local en el dispositivo, sin backend.
- **Autenticación:** ninguna; el uso es anónimo y local, en un solo dispositivo.
- **Moneda:** única, Soles peruanos (S/).
- **Ciclo de presupuesto:** mensual fijo por calendario.
- **Mercado objetivo:** producto destinado a cualquier familia, no a un hogar en particular. El catálogo inicial de categorías no contiene datos de una familia específica, y cada hogar puede adaptarlo en las dos direcciones: agregando las categorías que le falten y renombrando o eliminando las que no le sirvan (ver Alcance — Incluye, ítems 5 a 7). Es lo que permite, por ejemplo, que una familia sin vehículo se deshaga de las categorías de auto.
- **Categorías:** el catálogo inicial tiene 13 categorías predefinidas y es **ampliable y editable por el usuario**, sin diferencia de trato entre las predefinidas y las que él cree: puede renombrar y eliminar unas y otras. La única condición es la que declara el ítem 7 de Alcance — Incluye, que es la fuente de esa regla. Toda categoría tiene un tipo —gasto o ingreso— que se define al crearla y determina en qué total del resumen participa.
  - _Gasto (10):_ comida · internet · agua · luz · telefonía · gasolina · mantenimiento de auto · SAT (impuesto vehicular) · mantenimiento casa · otros
  - _Ingreso (3):_ sueldo 1 · sueldo 2 · otros ingresos
- **Idioma y audiencia:** español, público general no experto en finanzas.
- **Plazo:** sin fecha objetivo ni plazo comprometido para liberar el MVP. La priorización dentro del alcance no está condicionada por tiempo.
- **Arquitectura evolutiva (lineamiento):** el diseño debe permitir crecer por fases sin rehacer la base, contemplando una futura migración a multiusuario con backend y sincronización. Es un lineamiento sin criterio de verificación definido en esta fase: qué debe quedar preservado en esa migración (modelo de datos, identificación de movimientos, etc.) corresponde definirlo al rol de arquitectura, no a este PRD.

## Riesgos y Dependencias

**Dependencias:** no se identificaron dependencias externas para el MVP (no hay backend, servicios de terceros ni integraciones en alcance).

**Riesgos:**

- **Pérdida total de datos sin recuperación ni advertencia — riesgo aceptado sin mitigación.** Al no haber cuentas ni respaldo, si el usuario pierde, cambia o resetea el dispositivo, pierde todo su historial. El stakeholder decidió además no advertirlo dentro de la app (2026-09-15). Impacta directamente el criterio de retención D30: un usuario que pierde su historial difícilmente siga usando la app. Queda registrado para tenerlo presente al diseñar la fase de sincronización.
- **Tensión entre la personalización de categorías y la restricción de baja complejidad.** Las categorías personalizables estaban fuera del MVP en el brief y se incorporaron el 2026-09-16 para resolver una inconsistencia entre el catálogo cerrado y un mercado objetivo de cualquier familia. La decisión sumó **tres** capacidades al alcance de un MVP definido como deliberadamente pequeño: crear, renombrar y eliminar categorías. La cuarta capacidad de la sección, consultar el catálogo, no es atribuible a esta decisión: el MVP la necesitaba igual con catálogo cerrado, porque registrar un movimiento siempre exigió elegir su categoría, y se declaró en la v8 por precisión documental. El impacto, si la tensión se materializa, es que el MVP tarda más y llega con más superficie de producto que la necesaria para validar los dolores 1 y 2 del Problema, que es lo que el MVP existe para probar; y que la app deja de ser trivialmente simple para el público general no experto que define la audiencia. Mitigación ya ejecutada: las cuatro decisiones que la capacidad abría quedaron resueltas por el stakeholder el 2026-09-16, antes de construir, en vez de aparecer durante el desarrollo.
- **Categorías con movimientos en meses anteriores no se pueden eliminar nunca.** Es la consecuencia combinada de dos decisiones confirmadas: la eliminación de una categoría se impide mientras tenga movimientos en cualquier mes, y los movimientos solo se pueden eliminar dentro del mes en curso. Una categoría usada en un mes ya cerrado queda entonces de forma permanente en el catálogo, y el usuario solo puede renombrarla. No es un defecto de definición sino un efecto del alcance elegido; se registra para que el equipo no lo interprete como un error y para que se evalúe al diseñar la fase que habilite el acceso a meses anteriores.
- **Migración futura a multiusuario.** El salto a presupuesto compartido implica introducir cuentas, backend y sincronización sobre datos que nacieron locales y anónimos. El lineamiento de arquitectura evolutiva existe para mitigarlo, pero la estrategia de migración de los datos locales a una cuenta es una decisión de fase posterior, aún no tomada. Las categorías creadas por cada usuario agregan un caso a resolver en esa migración: cómo se reconcilian catálogos distintos entre miembros de una misma familia.
- **El MVP no valida el dolor de acuerdo familiar.** Por decisión del stakeholder, el uso compartido recién se prueba con multiusuario, así que el tercer dolor del Problema queda sin validar durante esta fase. El riesgo es construir la fase de multiusuario sobre una hipótesis no verificada acerca de cómo la familia acuerda su gasto.
- **Criterios de adopción autorreportados.** Al no haber instrumentación, los datos de uso sostenido y retención provienen de lo que reporten las familias participantes, no del producto. Están sujetos a sesgo de memoria y de deseabilidad, por lo que conviene leerlos como indicio y no como medición exacta.

## Criterios de éxito

**De usabilidad del MVP:**

- **Inmediatez de registro:** el usuario llega a la pantalla de registro de un movimiento con **1 toque** desde el inicio de la app, sin menús ni navegación intermedia. Los toques necesarios para completar monto y categoría no forman parte de este criterio, que mide el acceso y no el esfuerzo total de registro.
- **Comprensión de la pantalla principal:** en una prueba de usabilidad con **5 personas**, al menos **4 de 5 (80%)** entienden cómo va su mes sin necesidad de explicación.

**De adopción:**

- **Uso sostenido:** se registran **15 o más movimientos por semana** (≈2 por día) en el dispositivo de la familia participante.
- **Retención D30:** se siguen registrando movimientos **a los 30 días** de instalar la app.

**Método de verificación:** los criterios de adopción se validan con **10 familias**, mediante entrevistas y pruebas con usuarios, sin analítica ni telemetría en el producto. Cada familia participa con **un dispositivo y una persona registrando** —la única configuración posible en un MVP mono-usuario y local—, por lo que familia, dispositivo y usuario coinciden uno a uno a los fines de la medición. La ventana de seguimiento debe cubrir **al menos 30 días desde la instalación**, condición que se desprende del propio criterio de retención D30.

## Puntos Abiertos

Ninguno vigente. Los 13 Puntos Abiertos de las versiones 1 a 6 fueron resueltos por el stakeholder (9 el 2026-09-15 y 4 el 2026-09-16) y están reflejados en las secciones correspondientes.
