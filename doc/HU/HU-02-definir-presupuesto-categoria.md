# HU-02 — Definir el presupuesto mensual de una categoría

## Historia
Como usuario del hogar, quiero fijar o ajustar el monto presupuestado mensual de una categoría, para saber cuánto puedo gastar o esperar en esa categoría durante el mes.

## Alcance
Cubre la capacidad 2 de Alcance — Incluye: definir el presupuesto mensual de una categoría, sea del catálogo inicial o creada por el usuario. Fijar el monto de una categoría que no lo tiene y ajustar el de una que ya lo tiene son el mismo flujo, sin reglas diferenciadas. No incluye alertas al superar el presupuesto ni acumulación de saldo no gastado (fuera de alcance).

## Reglas de negocio
- Aplica a categorías de gasto e ingreso del catálogo vigente (predefinidas o propias).
- Es un único flujo: definir por primera vez y ajustar un monto existente no tienen reglas distintas.
- Moneda: S/.
- El presupuesto es mensual y del mes en curso (ciclo fijo por calendario).
- Persistencia local; sin cuentas.

## Criterios de aceptación (Gherkin)

### Escenario: Camino feliz — fijar presupuesto por primera vez
Dado que una categoría del catálogo no tiene monto presupuestado en el mes en curso
Cuando el usuario define un monto en S/ para esa categoría
Y confirma
Entonces esa categoría queda con ese presupuesto mensual
Y el resumen del mes puede contrastar gastado vs. presupuestado para ella

### Escenario: Ajustar un presupuesto ya definido
Dado que una categoría ya tiene un monto presupuestado en el mes en curso
Cuando el usuario cambia ese monto a otro valor en S/
Y confirma
Entonces el presupuesto de la categoría queda actualizado al nuevo monto
Y el avance gastado vs. presupuestado del resumen usa el monto nuevo

## Validación INVEST
- Independiente: no depende de crear/renombrar/eliminar categorías; opera sobre el catálogo vigente.
- Negociable: cómo se presenta el flujo (desde resumen o desde categoría) es negociable con UX.
- Valiosa: habilita el control por categoría del Objetivo.
- Estimable: un flujo de definición/ajuste de monto.
- Small/Pequeña: una sola capacidad, sin reglas diferenciadas entre alta y ajuste.
- Testeable: se puede verificar el monto guardado y su reflejo en el resumen.

## Puntos Abiertos
Ninguno.
