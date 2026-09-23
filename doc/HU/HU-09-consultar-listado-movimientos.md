# HU-09 — Consultar el listado de movimientos del mes en curso

## Historia
Como usuario del hogar, quiero ver el listado de movimientos del mes en curso, para revisar qué ingresos y gastos registré este mes.

## Alcance
Cubre la capacidad 9 de Alcance — Incluye: consultar el listado de movimientos del mes en curso. No incluye consultar movimientos de meses anteriores ni reportes históricos (fuera de alcance).

## Reglas de negocio
- Solo se listan movimientos del mes en curso.
- Cada movimiento refleja al menos monto, fecha, categoría (y nota si la tiene).
- Moneda S/. Persistencia local.
- Incluye movimientos de categorías predefinidas y propias.

## Criterios de aceptación (Gherkin)

### Escenario: Camino feliz — ver movimientos del mes
Dado que el usuario registró varios gastos e ingresos en el mes en curso
Cuando consulta el listado de movimientos del mes en curso
Entonces ve esos movimientos con monto en S/, fecha y categoría
Y no ve movimientos de meses anteriores

### Escenario: Mes sin movimientos
Dado que el mes en curso no tiene movimientos
Cuando consulta el listado
Entonces ve un listado vacío (o estado equivalente sin ítems)
Y no se muestran movimientos de otros meses

## Validación INVEST
- Independiente: consulta de lectura; no incluye editar/eliminar.
- Negociable: orden, filtros y presentación son de UX dentro del mes en curso.
- Valiosa: transparencia del registro diario.
- Estimable: listado acotado al mes en curso.
- Small/Pequeña: una sola capacidad.
- Testeable: presencia/ausencia de ítems y exclusión de otros meses.

## Puntos Abiertos
Ninguno.
