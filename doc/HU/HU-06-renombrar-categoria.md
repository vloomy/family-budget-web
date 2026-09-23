# HU-06 — Renombrar una categoría

## Historia
Como usuario del hogar, quiero renombrar una categoría propia o del catálogo inicial, para que el catálogo use los nombres que mi familia entiende.

## Alcance
Cubre la capacidad 6 de Alcance — Incluye: renombrar una categoría, propia o del catálogo inicial. No incluye cambiar el tipo de la categoría ni eliminarla.

## Reglas de negocio
- Se puede renombrar tanto categorías predefinidas como propias, sin diferencia de trato.
- El renombre no elimina ni recrea la categoría: conserva su identidad, tipo, presupuesto y movimientos asociados.
- Mientras una categoría tenga movimientos (en cualquier mes) y no se pueda eliminar, el usuario puede renombrarla (efecto documentado del alcance del PRD).
- Persistencia local.

## Criterios de aceptación (Gherkin)

### Escenario: Camino feliz — renombrar categoría del catálogo inicial
Dado que existe la categoría predefinida "comida"
Cuando el usuario la renombra a "alimentación"
Y confirma
Entonces el catálogo muestra "alimentación" en lugar de "comida"
Y el tipo, presupuesto y movimientos asociados se conservan

### Escenario: Renombrar categoría que tiene movimientos (no eliminable)
Dado que una categoría tiene movimientos registrados en algún mes
Y por ello no puede eliminarse
Cuando el usuario la renombra
Y confirma
Entonces el nuevo nombre queda aplicado
Y la categoría sigue existiendo con sus movimientos y presupuesto

## Validación INVEST
- Independiente: operación sobre una categoría existente; no requiere crear ni eliminar.
- Negociable: dónde se inicia el renombre es de UX.
- Valiosa: personalización del catálogo sin perder historial.
- Estimable: cambio de nombre con conservación de identidad.
- Small/Pequeña: una sola capacidad.
- Testeable: se verifica el nuevo nombre y la conservación de tipo/movimientos/presupuesto.

## Puntos Abiertos
Ninguno.
