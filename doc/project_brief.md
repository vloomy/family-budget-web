# Descripción del Problema — App Web de Presupuesto Familiar

_Documento de insumo para el Product Manager · Fecha: 2026-09-15 · Actualizado: 2026-09-24 (plataforma, stack y autenticación mono-usuario)_

> Este documento es un **brief de stakeholder**, no un PRD. Su propósito es dar al agente Product Manager el contexto de negocio necesario para redactar `PRD.md`. Los puntos abiertos del stakeholder (2026-09-15) y los del equipo (plataforma/stack e autenticación, 2026-09-24) están resueltos y reflejados en las secciones correspondientes (ver sección 10). No hay puntos abiertos vigentes.

---

## 1. Contexto

Muchas familias gestionan su dinero de forma informal: anotaciones sueltas, mensajes de chat, planillas dispersas o solo "de memoria". Esto hace difícil saber cuánto se gasta realmente, en qué, y si el mes va a cerrar en positivo o negativo. Las apps de finanzas existentes suelen ser complejas, orientadas a un solo usuario o cargadas de funciones que una familia promedio no necesita.

Queremos una **aplicación web simple** para que un grupo familiar registre sus ingresos y gastos, defina un presupuesto y vea de forma clara cómo va su mes.

## 2. Problema

Las familias no tienen una forma simple y compartida de:

- Registrar ingresos y gastos del día a día sin fricción.
- Saber cuánto pueden gastar por categoría (comida, transporte, servicios, etc.) antes de excederse.
- Ver, en cualquier momento, cuánto llevan gastado en el mes y cuánto les queda disponible.

El resultado es falta de visibilidad, sorpresas a fin de mes y dificultad para ponerse de acuerdo entre los miembros de la familia sobre en qué se gasta.

## 3. Usuarios / Actores (propuesta inicial)

- **Miembro de la familia (usuario principal):** registra gastos e ingresos, consulta el estado del presupuesto.
- **Administrador del hogar:** además de lo anterior, define el presupuesto por categoría y (a futuro) gestiona quién forma parte del grupo familiar.

> Decisión confirmada: el **MVP es de un solo usuario con cuenta propia**. Una persona crea su usuario, inicia sesión y mantiene el presupuesto familiar **solo para esa cuenta**; no puede compartirse con otros usuarios. La distinción administrador vs. miembro y el multiusuario compartido quedan como fase posterior (ver sección 7).

## 4. Objetivo de negocio

Que una familia pueda **entender y controlar su dinero mensual con poca fricción**, reemplazando planillas o anotaciones informales por una única herramienta simple y clara. El éxito se mide por que la familia registre sus movimientos con constancia y sepa en todo momento cómo va su presupuesto.

## 5. Propuesta de valor

- **Simple:** registrar un gasto toma segundos.
- **Claro:** una pantalla principal muestra el estado del mes de un vistazo.
- **Enfocado en la familia:** pensado para el uso compartido del hogar, no para un solo individuo ni para inversores/contabilidad avanzada.

## 6. Alcance sugerido del MVP

El MVP debe ser deliberadamente pequeño y entregar valor de punta a punta. Alcance confirmado por el stakeholder, con plataforma, stack y autenticación actualizados por el equipo (2026-09-24):

- Aplicación **web** con frontend en **React**.
- Backend con **Node (NestJS)**, base de datos **Neon (PostgreSQL)** y **Prisma** como ORM.
- Control de versiones en **GitHub**; CI/CD con **GitHub Actions**.
- **Crear usuario e iniciar sesión:** una persona tiene su cuenta; el presupuesto familiar de esa cuenta **no se comparte** con otros usuarios.
- Registrar **movimientos** (gasto o ingreso) con monto, fecha, categoría y nota opcional.
- Conjunto **predefinido de categorías** (ej. comida, transporte, servicios, salud, ocio, otros).
- Definir un **presupuesto mensual por categoría** (ciclo **mensual fijo** por calendario).
- **Pantalla resumen del mes:** total ingresado, total gastado, saldo disponible y avance por categoría (cuánto se lleva gastado vs. presupuestado).
- **Listado/historial** de movimientos del mes con posibilidad de editar y eliminar.
- Moneda única: **Soles peruanos (S/)**.
- Datos **persistidos en Neon (PostgreSQL)** a través del backend NestJS + Prisma, **aislados por cuenta de usuario**.

Todo lo listado en la sección 7 queda **fuera del MVP** (se aclara en el PRD como "No incluye por ahora").

## 7. Evolución incremental (post-MVP, a priorizar por el PM)

Funcionalidades candidatas para agregar de forma incremental una vez validado el MVP:

- **Multiusuario compartido:** varios miembros de la familia comparten y ven el mismo presupuesto en tiempo real (requiere modelo de hogar e invitaciones; las cuentas individuales ya existen en el MVP).
- **Categorías personalizables** por la familia.
- **Reportes y gráficos** de tendencias mensuales / históricos.
- **Gastos recurrentes** y recordatorios (alquiler, servicios, suscripciones).
- **Alertas** al acercarse o superar el presupuesto de una categoría.
- **Metas de ahorro.**
- **Exportar datos** (CSV / PDF).
- **Múltiples monedas** / soporte multi-idioma.
- **Adjuntar foto de comprobante** a un movimiento.

## 8. Restricciones y consideraciones conocidas

- Producto **web (React)** y **de baja complejidad**: priorizar simplicidad sobre cantidad de funciones.
- Stack de backend del MVP: **NestJS + Neon (PostgreSQL) + Prisma**.
- Herramientas de ingeniería: **GitHub** (control de versiones) y **GitHub Actions** (CI/CD).
- Autenticación del MVP: **cuenta individual** (crear usuario + iniciar sesión); presupuesto **no compartible**.
- El diseño debe permitir crecer por fases sin rehacer la base (arquitectura pensada para incrementos), incluyendo una futura fase de multiusuario sobre cuentas y backend ya existentes.
- Moneda única **Soles peruanos (S/)**.
- Público general (no expertos en finanzas): lenguaje y UX simples, en español.

## 9. Criterios de éxito (borrador para que el PM afine)

- Un usuario autenticado puede registrar un movimiento con poca fricción desde el inicio de la app.
- El usuario entiende, en la pantalla principal, cómo va su mes sin necesidad de explicación.
- **Uso sostenido (por usuario):** el usuario registra **al menos ~15 movimientos por semana** (≈2 por día), consistente con un uso mono-usuario en el MVP.
- **Retención:** el usuario sigue registrando movimientos **a los 30 días** de empezar a usar la app (retención D30).

## 10. Puntos Abiertos — RESUELTOS

Puntos confirmados por el stakeholder el 2026-09-15 (registro histórico). Donde el equipo del 2026-09-24 cambió o cerró la decisión, se indica:

1. **Plataforma objetivo del MVP:** ~~app multiplataforma para iOS y Android~~ → **aplicación web con frontend React** (equipo, 2026-09-24).
2. **Multiusuario en el MVP:** no; el presupuesto de una cuenta **no se comparte** con otros usuarios.
3. **Cuentas y autenticación:** ~~uso anónimo y local~~ → la persona **crea su usuario e inicia sesión**; el presupuesto queda aislado a esa cuenta (equipo / stakeholder, 2026-09-24).
4. **Período del presupuesto:** **mensual fijo** (calendario).
5. **Nivel mínimo de presupuesto:** **presupuesto por categoría**.
6. **Moneda:** **Soles peruanos (S/)**; una sola moneda es suficiente para el MVP.
7. **Manejo de datos y privacidad:** ~~almacenamiento local en el dispositivo (sin backend)~~ → **persistencia en Neon (PostgreSQL) vía NestJS + Prisma**, aislada por cuenta (equipo, 2026-09-24).
8. **Métrica de uso sostenido:** **~15 movimientos por semana por usuario** (≈2/día) + **retención a 30 días (D30)**.
9. **Control de versiones y CI/CD:** **GitHub** y **GitHub Actions** (equipo, 2026-09-24).
