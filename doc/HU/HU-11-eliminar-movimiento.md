# HU-11 — Eliminar un movimiento del mes en curso

## Historia
Como usuario del hogar, quiero eliminar un movimiento del mes en curso, para quitar registros erróneos o que no corresponden.

## Alcance
Cubre la capacidad 11 de Alcance — Incluye: eliminar un movimiento del mes en curso. No incluye eliminar movimientos de meses anteriores (fuera de alcance). Esta limitación, combinada con la regla de categorías (HU-07), implica que una categoría usada solo en meses cerrados no podrá eliminarse nunca (riesgo documentado del PRD; no ampliar alcance).

## Reglas de negocio
- Solo se pueden eliminar movimientos del mes en curso.
- Al eliminar, el movimiento deja de existir en el listado y deja de participar en los totales del resumen.
- Persistencia local; moneda S/.
- Eliminar un movimiento puede habilitar la eliminación de su categoría solo si esa categoría queda sin movimientos en ningún mes; si aún tiene movimientos en meses cerrados, la categoría sigue sin poder eliminarse (HU-07).

## Criterios de aceptación (Gherkin)

### Escenario: Camino feliz — eliminar movimiento del mes en curso
Dado que existe un movimiento en el listado del mes en curso
Cuando el usuario lo elimina
Y confirma
Entonces el movimiento ya no aparece en el listado del mes en curso
Y los totales del resumen se actualizan sin ese monto

### Escenario: No se puede eliminar un movimiento de un mes anterior
Dado que un movimiento pertenece a un mes ya cerrado
Cuando el usuario opera en el MVP sobre el mes en curso
Entonces ese movimiento no está disponible para eliminación
Y solo puede eliminar movimientos del mes en curso

## Validación INVEST
- Independiente: baja de un movimiento del mes; no incluye editar.
- Negociable: confirmación y gestos de borrado son de UX.
- Valiosa: corrige el historial del mes sin ruido.
- Estimable: operación de baja acotada al mes en curso.
- Small/Pequeña: una sola capacidad.
- Testeable: ausencia en listado, impacto en totales y límite temporal.

## Puntos Abiertos
Ninguno.
