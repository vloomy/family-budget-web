# HU-05 — Crear una categoría propia

## Historia
Como usuario del hogar, quiero crear una categoría propia declarando si es de gasto o de ingreso, para adaptar el catálogo a las necesidades de mi familia.

## Alcance
Cubre la capacidad 6 de Alcance — Incluye: crear una categoría propia, declarando al crearla si es de gasto o de ingreso. El tipo determina en qué total del resumen participan sus movimientos. No incluye renombrar ni eliminar. Requiere usuario autenticado (HU-12).

## Reglas de negocio
- Al crear, el usuario declara el tipo: gasto o ingreso. El tipo no se redefine después en esta capacidad.
- El tipo determina en qué total del resumen participan los movimientos de esa categoría.
- La categoría creada pasa a formar parte del catálogo vigente, sin diferencia de trato respecto a las predefinidas para presupuesto, renombre y eliminación (sujeta a las reglas de esas capacidades).
- Persistencia en Neon vía backend; datos aislados por cuenta; moneda S/; español.

## Criterios de aceptación (Gherkin)

### Escenario: Camino feliz — crear categoría de gasto
Dado que el usuario está autenticado y gestionando categorías
Cuando crea una categoría con nombre "colegio" y tipo gasto
Y confirma
Entonces "colegio" queda en el catálogo como gasto
Y puede usarse al registrar movimientos y al definir presupuesto
Y sus movimientos futuros participan en el total gastado del resumen

### Escenario: Crear categoría de ingreso
Dado que el usuario está autenticado y creando una categoría
Cuando la crea con nombre "freelance" y tipo ingreso
Y confirma
Entonces "freelance" queda en el catálogo como ingreso
Y sus movimientos futuros participan en el total ingresado del resumen

## Validación INVEST
- Independiente: alta de categoría sin depender de renombrar/eliminar.
- Negociable: formulario y validaciones de nombre duplicado (si aplica en UI) se negocian sin cambiar la capacidad.
- Valiosa: permite adaptar el catálogo a cualquier familia (restricción de mercado del PRD).
- Estimable: alta con nombre y tipo.
- Small/Pequeña: una sola capacidad.
- Testeable: se verifica presencia en catálogo, tipo y participación en totales.

## Puntos Abiertos
Ninguno.
