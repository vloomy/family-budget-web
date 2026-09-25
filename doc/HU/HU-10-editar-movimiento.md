# HU-10 — Editar un movimiento del mes en curso

## Historia
Como usuario del hogar, quiero editar un movimiento del mes en curso, para corregir monto, fecha, categoría o nota si me equivoqué al registrarlo.

## Alcance
Cubre la capacidad 11 de Alcance — Incluye: editar un movimiento del mes en curso. No incluye editar movimientos de meses anteriores (fuera de alcance). Requiere usuario autenticado (HU-12).

## Reglas de negocio
- Solo se pueden editar movimientos del mes en curso.
- Campos editables: monto, fecha, categoría y nota (nota sigue siendo opcional).
- Al cambiar de categoría, el tipo del movimiento (gasto/ingreso) queda determinado por el tipo de la nueva categoría, y los totales del resumen se recalculan en consecuencia.
- Moneda S/. Persistencia en Neon vía backend; datos aislados por cuenta.

## Criterios de aceptación (Gherkin)

### Escenario: Camino feliz — corregir monto y nota
Dado que el usuario está autenticado
Y existe un movimiento del mes en curso con monto S/ 50 y sin nota
Cuando el usuario lo edita a monto S/ 55 y agrega una nota
Y confirma
Entonces el movimiento queda actualizado con S/ 55 y la nota
Y el resumen del mes refleja los totales actualizados

### Escenario: No se puede editar un movimiento de un mes anterior
Dado que el usuario está autenticado
Y un movimiento pertenece a un mes ya cerrado
Cuando el usuario opera en el MVP sobre el mes en curso
Entonces ese movimiento no está disponible para edición
Y solo puede editar movimientos del mes en curso

## Validación INVEST
- Independiente: opera sobre un movimiento existente del mes; no incluye eliminar.
- Negociable: entrada al flujo de edición desde el listado es de UX.
- Valiosa: reduce fricción al corregir errores sin re-registrar.
- Estimable: edición de campos ya definidos en el alta.
- Small/Pequeña: una sola capacidad.
- Testeable: se verifica persistencia del cambio y límite al mes en curso.

## Puntos Abiertos
Ninguno.
