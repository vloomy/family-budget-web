# HU-08 — Consultar el resumen del mes en curso

## Historia
Como usuario del hogar, quiero ver el resumen del mes en curso con total ingresado, total gastado, saldo disponible y avance por categoría, para saber en todo momento cómo va el presupuesto del mes.

## Alcance
Cubre la capacidad 8 de Alcance — Incluye: consultar el resumen del mes en curso — total ingresado, total gastado, saldo disponible y avance por categoría (gastado vs. presupuestado), incluidas las categorías creadas por el usuario. No incluye reportes históricos, gráficos de tendencias ni alertas (fuera de alcance).

## Reglas de negocio
- Opera solo sobre el mes en curso.
- Totales: total ingresado (movimientos de categorías de ingreso), total gastado (movimientos de categorías de gasto), saldo disponible (relación entre ingresado y gastado del mes).
- Avance por categoría: gastado vs. presupuestado, incluyendo categorías propias del usuario.
- Moneda S/. Persistencia local. Español; audiencia no experta en finanzas.
- Criterio de usabilidad del PRD: en prueba con 5 personas, al menos 4 de 5 entienden cómo va su mes sin explicación (aplica a la pantalla principal / resumen).

## Criterios de aceptación (Gherkin)

### Escenario: Camino feliz — ver totales y avance del mes
Dado que en el mes en curso hay ingresos y gastos registrados
Y al menos una categoría de gasto tiene presupuesto definido
Cuando el usuario consulta el resumen del mes en curso
Entonces ve el total ingresado, el total gastado y el saldo disponible en S/
Y ve el avance gastado vs. presupuestado de las categorías con presupuesto

### Escenario: Incluye categorías creadas por el usuario
Dado que el usuario creó la categoría de gasto "colegio"
Y registró movimientos y/o presupuesto en "colegio" en el mes en curso
Cuando consulta el resumen
Entonces "colegio" participa en los totales según su tipo
Y su avance gastado vs. presupuestado se muestra si tiene presupuesto

### Escenario: Mes sin movimientos
Dado que el mes en curso no tiene movimientos registrados
Cuando el usuario consulta el resumen
Entonces ve totales en cero (o equivalentes a sin movimiento)
Y puede comprender el estado del mes sin datos previos

## Validación INVEST
- Independiente: consulta de lectura sobre datos ya persistidos; no incluye el alta de movimientos.
- Negociable: composición visual de la pantalla principal es de UX (sujeta al criterio 4 de 5).
- Valiosa: entrega el control del mes del Objetivo.
- Estimable: cuatro elementos de información definidos en el PRD.
- Small/Pequeña: una sola capacidad de consulta del mes en curso.
- Testeable: se verifican totales, saldo y avance; el criterio 4/5 se valida en prueba de usabilidad.

## Puntos Abiertos
Ninguno.
