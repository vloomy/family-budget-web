# HU-03 — Arrastre automático del presupuesto al mes siguiente

## Historia
Como usuario del hogar, quiero que al iniciar un nuevo mes se mantengan los montos presupuestados del mes anterior sin redefinirlos, para empezar el mes con el mismo plan sin trabajo extra.

## Alcance
Cubre la capacidad 4 de Alcance — Incluye: arrastre automático de los montos presupuestados al mes siguiente. El saldo no gastado no se acumula: el nuevo mes parte del mismo monto presupuestado, no del monto más el sobrante. No incluye acumulación de sobrante, reportes históricos ni acceso del usuario a meses anteriores (fuera de alcance). Requiere usuario autenticado (HU-12).

## Reglas de negocio
- Al iniciar un nuevo mes de calendario, los montos presupuestados del mes anterior se copian al mes nuevo sin acción del usuario.
- El saldo no gastado de una categoría se descarta al cerrar el mes; no se suma al presupuesto del mes nuevo.
- El usuario del MVP opera sobre el mes en curso; el arrastre es comportamiento automático del sistema.
- Persistencia en Neon vía backend; datos aislados por cuenta; moneda S/; ciclo mensual fijo.

## Criterios de aceptación (Gherkin)

### Escenario: Camino feliz — presupuestos se mantienen al cambiar de mes
Dado que el usuario está autenticado
Y en el mes anterior la categoría "comida" tenía un presupuesto de S/ 500
Y el mes de calendario ha cambiado al mes en curso
Cuando el usuario consulta el presupuesto de "comida" en el mes en curso
Entonces el monto presupuestado es S/ 500
Y no debió redefinir ese monto manualmente

### Escenario: El sobrante no se acumula
Dado que el usuario está autenticado
Y en el mes anterior la categoría "comida" tenía presupuesto S/ 500
Y solo se gastaron S/ 300 (sobrante S/ 200)
Y el mes de calendario ha cambiado
Cuando el usuario consulta el presupuesto de "comida" en el mes en curso
Entonces el presupuesto es S/ 500
Y no es S/ 700 ni incluye el sobrante del mes anterior

## Validación INVEST
- Independiente: complementa la definición de presupuesto (HU-02) como comportamiento de transición de mes; se puede probar aislada con datos de mes previo de la misma cuenta.
- Negociable: el momento exacto del arrastre (al abrir la app el día 1, al detectar cambio de mes) es detalle de implementación negociable.
- Valiosa: evita fricción mensual y sostiene el uso continuo.
- Estimable: regla de copia de montos y no acumulación de sobrante, clara en el PRD.
- Small/Pequeña: una sola capacidad de sistema.
- Testeable: se verifica el monto del nuevo mes y la ausencia de acumulación.

## Puntos Abiertos
Ninguno.
