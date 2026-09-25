# HU-12 — Crear cuenta e iniciar sesión

## Historia
Como persona del hogar, quiero crear mi usuario e iniciar sesión, para mantener el presupuesto familiar en una cuenta propia que no se comparte con otros usuarios.

## Alcance
Cubre la capacidad 1 de Alcance — Incluye: crear una cuenta de usuario e iniciar sesión. El presupuesto asociado a esa cuenta no puede compartirse con otros usuarios. No incluye multiusuario compartido, roles diferenciados, recuperación avanzada de acceso ni proveedores de identidad de terceros, salvo que el PRD los declare después.

## Reglas de negocio
- Una persona crea su cuenta e inicia sesión para usar la app.
- Los datos del presupuesto (movimientos, categorías, montos) quedan **aislados por cuenta**.
- El presupuesto de una cuenta **no se comparte** con otros usuarios en el MVP.
- Persistencia en Neon (PostgreSQL) vía NestJS + Prisma.
- Idioma: español.

## Criterios de aceptación (Gherkin)

### Escenario: Camino feliz — crear cuenta
Dado que la persona no tiene cuenta
Cuando completa el alta de usuario con los datos requeridos
Y confirma
Entonces su cuenta queda creada
Y puede iniciar sesión con ella

### Escenario: Camino feliz — iniciar sesión
Dado que la persona ya tiene una cuenta
Cuando inicia sesión con credenciales válidas
Entonces accede a su presupuesto familiar
Y no ve datos de otras cuentas

### Escenario: Presupuesto no compartible
Dado que el usuario A está autenticado con su cuenta
Y el usuario B tiene otra cuenta distinta
Cuando cada uno consulta su resumen del mes
Entonces cada uno ve solo los datos de su propia cuenta
Y no puede acceder al presupuesto del otro

## Validación INVEST
- Independiente: habilita el resto de HUs que asumen usuario autenticado; no depende de movimientos ni categorías.
- Negociable: campos concretos del alta y del login se negocian con UX/arquitectura sin cambiar la capacidad (cuenta individual no compartible).
- Valiosa: aísla datos por hogar/persona y habilita persistencia remota con identidad.
- Estimable: alta de cuenta + inicio de sesión + aislamiento por cuenta.
- Small/Pequeña: una sola capacidad de autenticación mono-usuario.
- Testeable: escenarios de alta, login y no cruce de datos entre cuentas.

## Puntos Abiertos
Ninguno de negocio. El detalle de campos de credenciales (p. ej. email/contraseña u otro) lo define UX/arquitectura sin ampliar el alcance.
