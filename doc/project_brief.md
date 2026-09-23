# Descripción del Problema — App Móvil de Presupuesto Familiar

_Documento de insumo para el Product Manager · Fecha: 2026-09-15 · Actualizado: 2026-09-15 (Puntos Abiertos resueltos por el stakeholder)_

> Este documento es un **brief de stakeholder**, no un PRD. Su propósito es dar al agente Product Manager el contexto de negocio necesario para redactar `PRD.md`. Todos los puntos abiertos originales fueron resueltos por el stakeholder y ya están reflejados en las secciones correspondientes (ver sección 10).

---

## 1. Contexto

Muchas familias gestionan su dinero de forma informal: anotaciones sueltas, mensajes de chat, planillas dispersas o solo "de memoria". Esto hace difícil saber cuánto se gasta realmente, en qué, y si el mes va a cerrar en positivo o negativo. Las apps de finanzas existentes suelen ser complejas, orientadas a un solo usuario o cargadas de funciones que una familia promedio no necesita.

Queremos una **aplicación móvil simple** para que un grupo familiar registre sus ingresos y gastos, defina un presupuesto y vea de forma clara cómo va su mes.

## 2. Problema

Las familias no tienen una forma simple y compartida de:

- Registrar ingresos y gastos del día a día sin fricción.
- Saber cuánto pueden gastar por categoría (comida, transporte, servicios, etc.) antes de excederse.
- Ver, en cualquier momento, cuánto llevan gastado en el mes y cuánto les queda disponible.

El resultado es falta de visibilidad, sorpresas a fin de mes y dificultad para ponerse de acuerdo entre los miembros de la familia sobre en qué se gasta.

## 3. Usuarios / Actores (propuesta inicial)

- **Miembro de la familia (usuario principal):** registra gastos e ingresos, consulta el estado del presupuesto.
- **Administrador del hogar:** además de lo anterior, define el presupuesto por categoría y (a futuro) gestiona quién forma parte del grupo familiar.

> Decisión confirmada: el **MVP es de un solo dispositivo/usuario**, con un único perfil sin distinción de roles y sin cuentas (uso anónimo y local). La distinción administrador vs. miembro y el multiusuario compartido quedan como fase posterior (ver sección 7).

## 4. Objetivo de negocio

Que una familia pueda **entender y controlar su dinero mensual en pocos toques**, reemplazando planillas o anotaciones informales por una única herramienta simple y clara. El éxito se mide por que la familia registre sus movimientos con constancia y sepa en todo momento cómo va su presupuesto.

## 5. Propuesta de valor

- **Simple:** registrar un gasto toma segundos.
- **Claro:** una pantalla principal muestra el estado del mes de un vistazo.
- **Enfocado en la familia:** pensado para el uso compartido del hogar, no para un solo individuo ni para inversores/contabilidad avanzada.

## 6. Alcance sugerido del MVP

El MVP debe ser deliberadamente pequeño y entregar valor de punta a punta. Alcance confirmado por el stakeholder:

- App **móvil multiplataforma** para **iOS y Android** (una sola base de código).
- Uso **anónimo y local**, de **un solo dispositivo/usuario**, sin registro ni login.
- Registrar **movimientos** (gasto o ingreso) con monto, fecha, categoría y nota opcional.
- Conjunto **predefinido de categorías** (ej. comida, transporte, servicios, salud, ocio, otros).
- Definir un **presupuesto mensual por categoría** (ciclo **mensual fijo** por calendario).
- **Pantalla resumen del mes:** total ingresado, total gastado, saldo disponible y avance por categoría (cuánto se lleva gastado vs. presupuestado).
- **Listado/historial** de movimientos del mes con posibilidad de editar y eliminar.
- Moneda única: **Soles peruanos (S/)**.
- Datos **guardados localmente en el dispositivo** (sin backend ni sincronización).

Todo lo listado en la sección 7 queda **fuera del MVP** (se aclara en el PRD como "No incluye por ahora").

## 7. Evolución incremental (post-MVP, a priorizar por el PM)

Funcionalidades candidatas para agregar de forma incremental una vez validado el MVP:

- **Sincronización y multiusuario:** varios miembros de la familia comparten y ven el mismo presupuesto en tiempo real (requiere cuentas y backend).
- **Categorías personalizables** por la familia.
- **Reportes y gráficos** de tendencias mensuales / históricos.
- **Gastos recurrentes** y recordatorios (alquiler, servicios, suscripciones).
- **Alertas** al acercarse o superar el presupuesto de una categoría.
- **Metas de ahorro.**
- **Exportar datos** (CSV / PDF).
- **Múltiples monedas** / soporte multi-idioma.
- **Adjuntar foto de comprobante** a un movimiento.

## 8. Restricciones y consideraciones conocidas

- Producto **móvil multiplataforma (iOS y Android)** y **de baja complejidad**: priorizar simplicidad sobre cantidad de funciones.
- El diseño debe permitir crecer por fases sin rehacer la base (arquitectura pensada para incrementos), incluyendo una futura migración a multiusuario con backend/sincronización.
- **Almacenamiento local** en el dispositivo para el MVP (sin backend).
- Moneda única **Soles peruanos (S/)**.
- Público general (no expertos en finanzas): lenguaje y UX simples, en español.

## 9. Criterios de éxito (borrador para que el PM afine)

- Un usuario puede registrar un movimiento en pocos toques desde que abre la app.
- El usuario entiende, en la pantalla principal, cómo va su mes sin necesidad de explicación.
- **Uso sostenido (por usuario/dispositivo):** el usuario registra **al menos ~15 movimientos por semana** (≈2 por día), consistente con un uso mono-usuario/mono-dispositivo en el MVP.
- **Retención:** el usuario sigue registrando movimientos **a los 30 días** de instalar la app (retención D30).

## 10. Puntos Abiertos — RESUELTOS

Todos los puntos abiertos fueron confirmados por el stakeholder el 2026-09-15 y ya están reflejados en las secciones anteriores. Se conservan aquí como registro de decisión:

1. **Plataforma objetivo del MVP:** app **multiplataforma para iOS y Android**.
2. **Multiusuario en el MVP:** no; el MVP es de **un solo dispositivo/usuario**.
3. **Cuentas y autenticación:** uso **anónimo y local**, sin registro ni login.
4. **Período del presupuesto:** **mensual fijo** (calendario).
5. **Nivel mínimo de presupuesto:** **presupuesto por categoría**.
6. **Moneda:** **Soles peruanos (S/)**; una sola moneda es suficiente para el MVP.
7. **Manejo de datos y privacidad:** **almacenamiento local** en el dispositivo (sin backend ni respaldo en el MVP).
8. **Métrica de uso sostenido:** ajustada a la escala mono-usuario/mono-dispositivo del MVP → **~15 movimientos por semana por usuario** (≈2/día) + **retención a 30 días (D30)**. Reemplaza el valor inicial de 100 movimientos/semana, poco realista para un único dispositivo.
