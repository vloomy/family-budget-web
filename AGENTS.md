# AGENTS.md — family-budget-web

Mapa operativo para agentes que trabajen en este repositorio. No duplica el PRD ni las Historias de Usuario: apunta a las fuentes de verdad y fija reglas que no deben asumirse.

## 1. Project Overview

App móvil de **presupuesto familiar** para que un usuario del hogar registre ingresos y gastos, defina presupuesto por categoría y vea cómo va el mes.

- **Problema que ataca el MVP:** fricción al registrar movimientos y falta de visibilidad del gasto por categoría. El acuerdo entre miembros de la familia queda diferido a multiusuario (fuera del MVP).
- **MVP:** un solo dispositivo/usuario, uso anónimo y local, sin cuentas ni backend, moneda **Soles peruanos (S/)**, ciclo **mensual fijo**, operación sobre el **mes en curso**.
- **Audiencia:** público general hispanohablante, no experto en finanzas. Producto para cualquier familia (no un hogar particular).

Detalle de alcance, actores, criterios de éxito y exclusiones: [`doc/PRD.md`](doc/PRD.md).

## 2. Repository Structure

```
family-budget-web/
├── AGENTS.md                 ← este archivo
├── README.md
└── doc/
    ├── project_brief.md      ← brief de stakeholder (insumo)
    ├── PRD.md                ← alcance vigente
    ├── PRD-Auditoria.md      ← auditoría formal del PRD
    └── HU/                   ← Historias de Usuario (una por capacidad)
```

**Importante**

- Trabajar sobre `doc/` para producto y requisitos.
- No inventar carpetas de código ni stack: aún no hay implementación de la app.
- No ampliar alcance “por buena práctica” si no está en el PRD o en las HUs.

## 3. Product docs & source of truth

| Tema | Fuente |
|------|--------|
| Alcance, actores, criterios, exclusiones | [`doc/PRD.md`](doc/PRD.md) |
| Insumo original del stakeholder | [`doc/project_brief.md`](doc/project_brief.md) |
| Historias de Usuario y escenarios Gherkin | [`doc/HU/`](doc/HU/) |
| Dictamen de calidad formal del PRD | [`doc/PRD-Auditoria.md`](doc/PRD-Auditoria.md) |

Si hay conflicto entre brief y PRD, **gana el PRD**. Si hay conflicto entre PRD y una HU, **escalar al Product Manager**; no “arreglar” el alcance en la HU.

## 4. Team agents (Herdr)

Orquestación del equipo de producto en esta sesión:

| Rol | Artefacto | Entrada |
|-----|-----------|---------|
| Product Manager | `doc/PRD.md` | brief / stakeholder |
| Product Manager Auditor | `doc/PRD-Auditoria.md` | PRD |
| Business Analyst | `doc/HU/*.md` | PRD |
| UX Designer | (aún no) | HUs — **handoff retenido** hasta autorización explícita |

Flujo: Brief → PRD → Auditoría → HUs → (UX pendiente de autorización).

En Herdr, dirigir agentes por `pane_id` (no por título con espacios). Ambigüedades de negocio: escalar al PM, no asumir.

## 5. Tech Stack

**Pendiente — no inventar.**

Cualquier stack futuro debe respetar las restricciones de producto ya confirmadas:

- Móvil **multiplataforma** (iOS y Android), una sola base de código.
- **Almacenamiento local** en el dispositivo; sin backend en el MVP.
- Sin autenticación / cuentas en el MVP.
- UI y copy en **español**; moneda **S/**.

Cuando se elija stack, completar esta sección (runtime, framework, persistencia local, testing, package manager).

## 6. Development Workflow

**Pendiente** hasta que exista código y herramientas de build.

Hasta entonces, el “workflow” de agentes es documental: leer PRD/HU relevantes → proponer o editar artefactos en `doc/` → no implementar app sin decisión de stack.

## 7. Architecture Rules (producto)

Reglas confirmadas que cualquier diseño o implementación debe respetar:

- Solo el **mes en curso** es editable/consultable por el usuario (movimientos).
- El presupuesto se **arrastra** al mes siguiente; el **sobrante no se acumula**.
- Categorías tipadas (**gasto** o **ingreso**); catálogo inicial de 13 + creación/renombrado/eliminación por el usuario.
- **No eliminar** una categoría si tiene movimientos en **cualquier** mes (efecto: categorías usadas en meses cerrados solo se pueden renombrar).
- Sin analítica/telemetría; sin aviso in-app de ausencia de respaldo (riesgo aceptado).
- Priorizar **simplicidad** sobre cantidad de funciones.
- Diseño pensado para crecer a multiusuario/backend **sin** rehacer la base (lineamiento; concreción futura de arquitectura).

## 8. Agent Instructions

**Antes de modificar**

- Leer las secciones del PRD y las HUs afectadas.
- Confirmar que el cambio no contradice Alcance — No incluye.

**Nunca asumir**

- Stack, librerías o estructura de código de la app.
- Funcionalidades post-MVP (multiusuario, alertas, históricos, export, etc.).
- Umbrales o categorías no escritas en el PRD.

**Pedir confirmación**

- Cualquier cambio de alcance o nueva capacidad.
- Handoff a UX (hoy **no autorizado**).
- Commits o push, salvo pedido explícito del usuario.

**Después**

- Dejar artefactos en las rutas canónicas (`doc/PRD.md`, `doc/HU/`, etc.).
- Si falta un dato de negocio: Punto Abierto con pregunta exacta y destinatario; no elegir “la opción más común”.

## 9. Definition of Done

**Tareas de producto / documentación**

- Artefacto en la ruta correcta bajo `doc/`.
- Sin contenido de negocio inventado.
- Consistente con PRD y HUs existentes.
- Escalaciones de alcance resueltas o abiertas explícitamente.

**Tareas de código (cuando exista implementación)**

- Completar esta sección con tests, lint, build y criterios de merge. Hasta entonces no aplica.
