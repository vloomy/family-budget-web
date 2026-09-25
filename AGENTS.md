# AGENTS.md — family-budget-web

Mapa operativo para agentes que trabajen en este repositorio. No duplica el PRD ni las Historias de Usuario: apunta a las fuentes de verdad y fija reglas que no deben asumirse.

## 1. Project Overview

App **web** de **presupuesto familiar** para que un usuario del hogar registre ingresos y gastos, defina presupuesto por categoría y vea cómo va el mes.

- **Problema que ataca el MVP:** fricción al registrar movimientos y falta de visibilidad del gasto por categoría. El acuerdo entre miembros de la familia queda diferido a multiusuario (fuera del MVP).
- **MVP:** aplicación web, **cuenta individual** (crear usuario e iniciar sesión; presupuesto **no compartible**), moneda **Soles peruanos (S/)**, ciclo **mensual fijo**, operación sobre el **mes en curso**.
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
    └── HU/                   ← Historias de Usuario (HU-01…HU-12; una por capacidad del PRD)
```

**Importante**

- Trabajar sobre `doc/` para producto y requisitos.
- Las HUs deben reflejar el PRD vigente: app **web**, cuenta individual (**HU-12**), persistencia **Neon vía NestJS + Prisma**, datos **aislados por cuenta**.
- No inventar carpetas de código ni stack más allá de lo confirmado en el PRD / sección 5.
- No ampliar alcance “por buena práctica” si no está en el PRD o en las HUs.

## 3. Product docs & source of truth

| Tema | Fuente |
|------|--------|
| Alcance, actores, criterios, exclusiones | [`doc/PRD.md`](doc/PRD.md) |
| Insumo original del stakeholder | [`doc/project_brief.md`](doc/project_brief.md) |
| Historias de Usuario y escenarios Gherkin | [`doc/HU/`](doc/HU/) |

Si hay conflicto entre brief y PRD, **gana el PRD**. Si hay conflicto entre PRD y una HU, **escalar al Product Manager**; no “arreglar” el alcance en la HU.

## 4. Team agents (Herdr)

Orquestación del equipo de producto en esta sesión:

| Rol | Artefacto | Entrada |
|-----|-----------|---------|
| Product Manager | `doc/PRD.md` | brief / stakeholder |
| Business Analyst | `doc/HU/*.md` | PRD |
| UX Designer | (aún no) | HUs — **handoff retenido** hasta autorización explícita |

Flujo: Brief → PRD → HUs → (UX pendiente de autorización).

En Herdr, dirigir agentes por `pane_id` (no por título con espacios). Ambigüedades de negocio: escalar al PM, no asumir.

## 5. Tech Stack

Confirmado para el MVP (detalle de librerías y despliegue: arquitectura):

- **Frontend:** aplicación web con **React**.
- **Backend:** **NestJS (Node)** + **Neon (PostgreSQL)** + **Prisma** (ORM).
- **Ingeniería:** **GitHub** (control de versiones) y **GitHub Actions** (CI/CD).
- **Autenticación:** cuenta individual; datos aislados por usuario; sin compartir presupuesto en el MVP.
- UI y copy en **español**; moneda **S/**.

## 6. Development Workflow

**Pendiente** hasta que existan herramientas de build en el repo.

Hasta entonces, el “workflow” de agentes es documental: leer PRD/HU relevantes → proponer o editar artefactos en `doc/` → no implementar app sin alinear con el stack confirmado.

## 7. Architecture Rules (producto)

Reglas confirmadas que cualquier diseño o implementación debe respetar:

- Solo el **mes en curso** es editable/consultable por el usuario (movimientos).
- El presupuesto se **arrastra** al mes siguiente; el **sobrante no se acumula**.
- Categorías tipadas (**gasto** o **ingreso**); catálogo inicial de 13 + creación/renombrado/eliminación por el usuario.
- **No eliminar** una categoría si tiene movimientos en **cualquier** mes (efecto: categorías usadas en meses cerrados solo se pueden renombrar).
- Datos **aislados por cuenta**; el presupuesto **no se comparte** entre usuarios en el MVP.
- Las capacidades del MVP (excepto crear cuenta / login) asumen **usuario autenticado**.
- Sin analítica/telemetría.
- Priorizar **simplicidad** sobre cantidad de funciones.
- Diseño pensado para crecer a multiusuario compartido **sin** rehacer la base (lineamiento; concreción futura de arquitectura).

## 8. Agent Instructions

**Antes de modificar**

- Leer las secciones del PRD y las HUs afectadas.
- Confirmar que el cambio no contradice Alcance — No incluye.

**Nunca asumir**

- Librerías o estructura de código no escritas en el PRD / stack confirmado.
- Funcionalidades post-MVP (multiusuario compartido, alertas, históricos, export, etc.).
- Umbrales o categorías no escritas en el PRD.
- Campos concretos de registro (email, OAuth, etc.) si no están en el PRD o en una HU.

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
