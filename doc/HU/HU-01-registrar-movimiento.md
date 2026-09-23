# HU-01 — Registrar un movimiento

## Historia
Como usuario del hogar, quiero registrar un gasto o un ingreso con monto, fecha, categoría y nota opcional, para llevar el control diario del dinero sin anotaciones informales.

## Alcance
Cubre la capacidad 1 de Alcance — Incluye: registrar un movimiento (gasto o ingreso) con monto, fecha, categoría y nota opcional. No incluye editar ni eliminar movimientos (HUs posteriores), ni adjuntar foto de comprobante (fuera de alcance).

## Reglas de negocio
- El movimiento es de tipo gasto o ingreso según el tipo de la categoría elegida.
- Campos obligatorios: monto, fecha, categoría. Nota es opcional.
- Moneda única: Soles peruanos (S/).
- Persistencia local en el dispositivo; sin cuentas ni sincronización.
- El registro opera sobre el mes en curso (ciclo mensual fijo por calendario).
- Criterio de usabilidad del PRD: desde el inicio de la app, el usuario llega a la pantalla de registro con 1 toque, sin menús ni navegación intermedia.

## Criterios de aceptación (Gherkin)

### Escenario: Camino feliz — registrar un gasto
Dado que el usuario está en el inicio de la app
Y existe al menos una categoría de gasto en el catálogo
Cuando llega a la pantalla de registro con 1 toque
Y completa monto, fecha, una categoría de gasto y opcionalmente una nota
Y confirma el registro
Entonces el movimiento queda guardado localmente como gasto
Y aparece en el listado y en los totales del mes en curso

### Escenario: Camino feliz — registrar un ingreso
Dado que el usuario está en la pantalla de registro
Y existe al menos una categoría de ingreso en el catálogo
Cuando completa monto, fecha y una categoría de ingreso
Y confirma el registro
Entonces el movimiento queda guardado localmente como ingreso
Y participa en el total ingresado del mes en curso

### Escenario: Nota opcional omitida
Dado que el usuario está en la pantalla de registro
Cuando completa monto, fecha y categoría sin ingresar nota
Y confirma el registro
Entonces el movimiento se guarda correctamente sin nota

## Validación INVEST
- Independiente: se puede entregar sin depender de editar/eliminar movimientos; requiere catálogo existente (predefinido o ya creado).
- Negociable: el flujo de captura y validaciones de UI se negocian con UX sin cambiar la capacidad.
- Valiosa: ataca el dolor de registro incompleto/abandonado del Problema.
- Estimable: alcance acotado a un formulario de alta con cuatro campos conocidos.
- Small/Pequeña: una sola capacidad — alta de movimiento.
- Testeable: escenarios Gherkin verificables en dispositivo local.

## Puntos Abiertos
Ninguno.
