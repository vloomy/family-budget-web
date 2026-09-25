# HU-04 — Consultar el catálogo de categorías

## Historia
Como usuario del hogar, quiero ver el catálogo de categorías vigente con su tipo (gasto o ingreso), para elegir y gestionar las categorías con las que registro y presupuesto.

## Alcance
Cubre la capacidad 5 de Alcance — Incluye: consultar el catálogo vigente, incluidas las creadas por el usuario y las que no tienen presupuesto ni movimientos en el mes. No incluye crear, renombrar ni eliminar (HUs 05–07). Requiere usuario autenticado (HU-12).

## Reglas de negocio
- El catálogo inicial tiene 13 categorías: 10 de gasto (comida, internet, agua, luz, telefonía, gasolina, mantenimiento de auto, SAT, mantenimiento casa, otros) y 3 de ingreso (sueldo 1, sueldo 2, otros ingresos).
- Se muestran también las categorías creadas por el usuario.
- Toda categoría tiene tipo gasto o ingreso.
- Se listan categorías aunque no tengan presupuesto ni movimientos en el mes en curso.
- Sin diferencia de trato visual de negocio entre predefinidas y propias respecto a su presencia en el catálogo.
- Idioma: español. Persistencia en Neon vía backend; datos aislados por cuenta.

## Criterios de aceptación (Gherkin)

### Escenario: Camino feliz — ver catálogo con tipos
Dado que el usuario está autenticado
Y su cuenta tiene el catálogo inicial de 13 categorías
Cuando el usuario consulta el catálogo de categorías
Entonces ve las categorías vigentes con su tipo (gasto o ingreso)
Y puede distinguir las de gasto de las de ingreso

### Escenario: Incluye categorías sin presupuesto ni movimientos y las propias
Dado que el usuario está autenticado
Y creó una categoría propia "colegio"
Y existe una categoría del catálogo sin presupuesto ni movimientos en el mes en curso
Cuando consulta el catálogo
Entonces "colegio" aparece en el listado con su tipo
Y la categoría sin presupuesto ni movimientos también aparece

## Validación INVEST
- Independiente: consulta de solo lectura; no depende de create/rename/delete para entregarse con el catálogo inicial.
- Negociable: layout y agrupación son de UX.
- Valiosa: base para registrar movimientos y gestionar categorías.
- Estimable: listado con tipo y cobertura del catálogo vigente.
- Small/Pequeña: una sola capacidad de consulta.
- Testeable: se verifica presencia, tipo y categorías sin uso en el mes.

## Puntos Abiertos
Ninguno.
