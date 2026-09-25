# HU-07 — Eliminar una categoría

## Historia
Como usuario del hogar, quiero eliminar una categoría propia o del catálogo inicial cuando no tenga movimientos en ningún mes, para quitar del catálogo las que mi familia no usa.

## Alcance
Cubre la capacidad 8 de Alcance — Incluye: eliminar una categoría, propia o del catálogo inicial, solo si no tiene movimientos registrados en ningún mes. Mientras los tenga, la eliminación se impide; el usuario puede renombrarla (HU-06). No incluye acceso del usuario a eliminar movimientos de meses anteriores (fuera de alcance). Requiere usuario autenticado (HU-12).

## Reglas de negocio
- Se puede intentar eliminar categorías predefinidas y propias, sin diferencia de trato.
- Condición de eliminación: la categoría no debe tener movimientos registrados en ningún mes (no solo en el mes en curso).
- Si tiene movimientos en cualquier mes, la eliminación se impide; el usuario puede renombrarla.
- Consecuencia del alcance del MVP (riesgo documentado, no defecto): si una categoría tiene movimientos solo en meses ya cerrados, el usuario no puede eliminar esos movimientos (el MVP solo permite eliminar movimientos del mes en curso), por lo que esa categoría no se podrá eliminar nunca; solo podrá renombrarse.
- La verificación de movimientos en meses anteriores es interna del sistema; no implica dar al usuario acceso a consultar o editar meses anteriores.
- Persistencia en Neon vía backend; datos aislados por cuenta.

## Criterios de aceptación (Gherkin)

### Escenario: Camino feliz — eliminar categoría sin movimientos
Dado que el usuario está autenticado
Y la categoría "gasolina" no tiene movimientos registrados en ningún mes
Cuando el usuario solicita eliminarla
Y confirma
Entonces la categoría deja de aparecer en el catálogo vigente
Y ya no está disponible para nuevos registros ni presupuestos

### Escenario: Eliminación impedida si tiene movimientos en cualquier mes
Dado que el usuario está autenticado
Y la categoría "comida" tiene al menos un movimiento registrado en algún mes
Cuando el usuario solicita eliminarla
Entonces la eliminación se impide
Y la categoría permanece en el catálogo
Y el usuario puede renombrarla

### Escenario: Categoría con movimientos solo en mes cerrado no se puede eliminar
Dado que el usuario está autenticado
Y una categoría tiene movimientos únicamente en un mes ya cerrado
Y no tiene movimientos en el mes en curso
Cuando el usuario solicita eliminarla
Entonces la eliminación se impide
Y la categoría permanece en el catálogo (solo puede renombrarse)

## Validación INVEST
- Independiente: regla de baja clara; complementa pero no requiere entregar renombrar en el mismo incremento para ser testeable la impedimento.
- Negociable: mensaje y UX del impedimento son de UX; la regla de negocio no.
- Valiosa: permite adaptar el catálogo quitando lo que no sirve, con integridad de historial.
- Estimable: condición binaria (tiene / no tiene movimientos en cualquier mes).
- Small/Pequeña: una sola capacidad.
- Testeable: escenarios de baja permitida e impedida, incluido el caso de mes cerrado.

## Puntos Abiertos
Ninguno.
