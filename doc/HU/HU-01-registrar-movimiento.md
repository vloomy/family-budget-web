# HU-01 — Registrar un movimiento

## Historia
Como usuario del hogar, quiero registrar un gasto o un ingreso con monto, fecha, categoría y nota opcional, para llevar el control diario del dinero sin anotaciones informales.

## Alcance
Cubre la capacidad 2 de Alcance — Incluye: registrar un movimiento (gasto o ingreso) con monto, fecha, categoría y nota opcional. No incluye editar ni eliminar movimientos (HUs posteriores), ni adjuntar foto de comprobante (fuera de alcance). Requiere usuario autenticado (HU-12).

## Reglas de negocio
- El movimiento es de tipo gasto o ingreso según el tipo de la categoría elegida.
- Campos obligatorios: monto, fecha, categoría. Nota es opcional.
- Moneda única: Soles peruanos (S/).
- Persistencia en Neon vía backend; datos aislados por cuenta del usuario autenticado.
- El registro opera sobre el mes en curso (ciclo mensual fijo por calendario).
- Criterio de usabilidad del PRD: el usuario ya autenticado llega a la pantalla de registro con 1 clic desde el inicio de la app, sin menús ni navegación intermedia.

## Criterios de aceptación (Gherkin)

### Escenario: Camino feliz — registrar un gasto
Dado que el usuario está autenticado y en el inicio de la app
Y existe al menos una categoría de gasto en el catálogo
Cuando llega a la pantalla de registro con 1 clic
Y completa monto, fecha, una categoría de gasto y opcionalmente una nota
Y confirma el registro
Entonces el movimiento queda guardado en su cuenta como gasto
Y aparece en el listado y en los totales del mes en curso

### Escenario: Camino feliz — registrar un ingreso
Dado que el usuario está autenticado y en la pantalla de registro
Y existe al menos una categoría de ingreso en el catálogo
Cuando completa monto, fecha y una categoría de ingreso
Y confirma el registro
Entonces el movimiento queda guardado en su cuenta como ingreso
Y participa en el total ingresado del mes en curso

### Escenario: Nota opcional omitida
Dado que el usuario está autenticado y en la pantalla de registro
Cuando completa monto, fecha y categoría sin ingresar nota
Y confirma el registro
Entonces el movimiento se guarda correctamente sin nota

## Validación INVEST
- Independiente: se puede entregar sin depender de editar/eliminar movimientos; requiere catálogo existente (predefinido o ya creado).
- Negociable: el flujo de captura y validaciones de UI se negocian con UX sin cambiar la capacidad.
- Valiosa: ataca el dolor de registro incompleto/abandonado del Problema.
- Estimable: alcance acotado a un formulario de alta con cuatro campos conocidos.
- Small/Pequeña: una sola capacidad — alta de movimiento.
- Testeable: escenarios Gherkin verificables con usuario autenticado y persistencia por cuenta.

## Puntos Abiertos
Ninguno.
