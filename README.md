# Portfolio de Ingeniería de Software

**Autor:** **Pendiente:** nombre y presentación personal `<!-- TODO:nombre -->`

> Construyo productos de software de punta a punta: modelado de dominio, APIs, interfaces y automatización con IA.

**Contacto:** **Pendiente:** canales de contacto (email, LinkedIn, …) `<!-- TODO:contacto -->`

---

## Tabla de contenidos

- [Sobre mí y stack técnico](#sobre-mí-y-stack-técnico)
- [Proyectos](#proyectos)
  - [Multimax CRM](#multimax-crm)
  - [OdontoSoft](#odontosoft)
  - [PostuLog](#postulog)
  - [Places](#places)
- [Convenciones del README](#convenciones-del-readme)

---

## Sobre mí y stack técnico

Este repositorio reúne cuatro proyectos que abarcan el ciclo completo de un producto: modelado de datos, APIs, interfaces de usuario, automatización con IA e infraestructura. Las tecnologías que atraviesan los proyectos son:

- **Backend:** Python + FastAPI (async), Node.js + Express, SQLAlchemy 2.0, Drizzle ORM, Prisma ORM.
- **Frontend:** React, Next.js, Vite, TypeScript, Tailwind CSS, Zustand, Radix UI.
- **Datos:** PostgreSQL, pgvector, SQLite, Redis, Alembic y migraciones versionadas.
- **IA y automatización:** LLM con tool calling / function calling (DeepSeek, Anthropic), embeddings y búsqueda semántica, limpieza de contenido web (`trafilatura`).
- **Infraestructura y calidad:** Docker Compose, autenticación JWT + RBAC, pruebas con pytest y Vitest, linters (Ruff, ESLint).

---

## Proyectos

### Multimax CRM

> **Pitch:** CRM operativo *mobile-first* para PyMEs de insumos de limpieza en Argentina, con precios diferenciados, WhatsApp automatizado y catálogo procesado por IA.

**Ficha** — **Tipo:** producto operativo B2B (PWA / mobile-first). **Alcance:** full-stack (React + Node.js/Express + datos + infra Docker). **Estado:** proyecto de portfolio.

**Stack:** `React` + `Vite` + `TypeScript` · `Tailwind CSS` (design system "Serene Air") · `Node.js` + `Express` + `TypeScript` · `Prisma ORM` · `BullMQ` + `Redis` · `SQLite` (dev) → `PostgreSQL` (prod, Docker) · `Docker Compose` · `JWT` + `RBAC`.

**Decisiones técnicas**

- **Bot de WhatsApp con máquina de estados (FSM):** la calificación de leads entrantes se modela como una FSM (saludo → rubro → zona → envío de lista de precios) en lugar de respuestas heurísticas, y cada conversación queda registrada en base de datos para auditoría.
- **Broadcast asíncrono con rate-limiting y jitter:** los envíos masivos se encolan en BullMQ/Redis y se espacian deliberadamente para evitar bloqueos del API de WhatsApp, separando la operación interactiva de la de mensajería.
- **Precios diferenciados por segmento:** el cálculo de precios (mayorista, minorista, distribuidor) se resuelve por multiplicadores de margen o precios fijos a nivel de cliente, evitando listas de precios duplicadas.
- **Trayectoria SQLite → PostgreSQL dockerizado:** el desarrollo corre sobre SQLite y la producción sobre PostgreSQL orquestado con Docker Compose, dejando un camino claro de escalado por concurrencia.
- **Extracción de catálogo con DeepSeek:** catálogos en PDF/imagen se convierten a datos estructurados (nombres, códigos, precios, presentaciones) con *preview* y actualización masiva de listas.

**Pendiente (captura):** se agregará una imagen del producto más adelante. `<!-- TODO:image:multimax-crm -->`

**Pendiente (repositorio):** se agregará el enlace al repositorio más adelante. `<!-- TODO:repo-link:multimax-crm -->`

**Detalle técnico completo:** [`multimax-crm.md`](./multimax-crm.md)

---

### OdontoSoft

> **Pitch:** SaaS web-first para la gestión clínica, operativa y administrativa de clínicas odontológicas pequeñas y medianas.

**Ficha** — **Tipo:** SaaS B2B multi-rol (web-first). **Alcance:** full-stack (React + Express/Drizzle + PostgreSQL). **Estado:** proyecto de portfolio.

**Stack:** `React 18` + `TypeScript` + `Vite` · `react-router-dom` (lazy loading) · `Zustand` · `Tailwind CSS` + `Radix UI` · `@dnd-kit` · `Node.js` + `Express 5` + `TypeScript` · `Drizzle ORM` · `PostgreSQL` · `Vitest` · `ESLint` + `tsc`.

**Decisiones técnicas**

- **Agenda multirrecurso con drag & drop y validación de conflictos:** la creación de turnos se hace por arrastre sobre celdas horarias (día/semana/mes) y se valida algorítmicamente el solapamiento de sillones y profesionales antes de persistir, en lugar de delegar la consistencia al backend.
- **RBAC con separación estricta clínica/administrativa:** solo `ODONTOLOGO` y `ADMIN` prescriben en evoluciones y editan el odontograma; solo `ADMIN` y `RECEPCION` acceden a finanzas y equipo, manteniendo la información clínica aislada de la administrativa.
- **Máquina de estados del turno con historial inmutable:** el ciclo de vida (`SIN_CONFIRMAR`, `CONFIRMADO`, `EN_SALA`, `ATENDIDO`, `AUSENTE`, `CANCELADO`, `REPROGRAMADO`) se acompaña de un `historialEstados` inmutable que da trazabilidad y auditoría.
- **Odontograma FDI interactivo:** registro gráfico y textual por pieza (permanentes y temporales) y por cara (oclusal, mesial, distal, vestibular, lingual/palatina) siguiendo la norma FDI.
- **Repositorio dual `mockRepo`/`httpRepo`:** la UI depende de una abstracción de repositorio que permite desarrollar en memoria (`mockRepo`) y conmutar a la API REST (`httpRepo`) sin acoplar las pantallas al backend.

**Pendiente (captura):** se agregará una imagen del producto más adelante. `<!-- TODO:image:odontosoft -->`

**Pendiente (repositorio):** se agregará el enlace al repositorio más adelante. `<!-- TODO:repo-link:odontosoft -->`

**Detalle técnico completo:** [`odontosoft.md`](./odontosoft.md)

---

### PostuLog

> **Pitch:** CRM personal de postulaciones laborales que extrae ofertas de empleo con LLM y *tool calling* forzado.

**Ficha** — **Tipo:** producto personal + pipeline de IA. **Alcance:** full-stack (FastAPI + React/Vite). **Estado:** proyecto de portfolio.

**Stack:** `Python 3.12` + `FastAPI` (async) · `SQLAlchemy 2.0` (async) · `PostgreSQL` (UUID + `JSONB`) · `Alembic` · `httpx` + `trafilatura` · `Pydantic v2` (tool use) · `React` + `Vite` + `TypeScript` · `Tailwind CSS` · `pytest` + `pytest-asyncio` + `respx` · `Ruff`.

**Decisiones técnicas**

- **Async por defecto:** todo el I/O (HTTP externo, consultas a PostgreSQL, invocaciones al LLM) es estrictamente asíncrono (`async def`, `httpx.AsyncClient`, SQLAlchemy async) para no bloquear el event loop.
- **Tool use forzado para extracción:** la extracción desde URLs o texto crudo nunca confía en *parsing* de texto libre; usa *function calling* con schemas Pydantic estrictos, garantizando datos tipados y deterministas (título, empresa, salario, modalidad, seniority, etc.).
- **Persistencia con UUID + `JSONB`:** claves primarias UUID y campos `JSONB` para metadatos flexibles e historial de cambios de estado, evitando migraciones por cada campo nuevo de auditoría.
- **Arquitectura en capas:** `routers` (HTTP + validación con DTOs), `services` (lógica de negocio y excepciones de dominio) y `models` (tablas relacionales), con las excepciones de dominio mapeadas a `HTTPException`.
- **Limpieza de contenido antes del LLM:** `trafilatura` descarta menús, anuncios y ruido de la página antes de enviar el texto al modelo, mejorando la señal y reduciendo tokens.

**Pendiente (captura):** se agregará una imagen del producto más adelante. `<!-- TODO:image:postulog -->`

**Pendiente (repositorio):** se agregará el enlace al repositorio más adelante. `<!-- TODO:repo-link:postulog -->`

**Detalle técnico completo:** [`postulog.md`](./postulog.md)

---

### Places

> **Pitch:** el *"Letterboxd"* de la gastronomía: una plataforma documental y museo digital para la crítica, preservación y memoria cultural culinaria.

**Ficha** — **Tipo:** plataforma social / archivo cultural. **Alcance:** full-stack (FastAPI + Next.js + ML/pgvector). **Estado:** proyecto de portfolio.

**Stack:** `Python 3.12` + `FastAPI` (async) · `SQLAlchemy 2.0` · `PostgreSQL` + `pgvector` (fallback `SQLite` en dev) · `Alembic` · `Pydantic v2` · `Next.js 14` (App Router) + `TypeScript` · `Tailwind CSS` + `Lucide`.

**Decisiones técnicas**

- **Cero *hard deletes*:** sobre las entidades cardinales (`Venue`, `Log`, `Review`, `Person`, `Event`) se prohíbe el `DELETE` físico y las bajas se gestionan con *soft-delete* auditado; un local cerrado pasa a estado `closed` pero su ficha permanece navegable y citable.
- **Búsqueda semántica con pgvector y fallback a SQLite:** los embeddings de reseñas se almacenan con la extensión `pgvector` para similitud coseno, con un soporte de desarrollo transparente sobre SQLite que no rompe el flujo local.
- **Calificación crítica ponderada (0.5–5.0):** un sistema de valoración con `Review`, fecha de consumo y metadatos de atmósfera/tags, en lugar de un simple promedio de estrellas.
- **Entidad `Person` + `VenueCrewRole`:** chefs, bartenders, pasteleros y sommeliers son entidades independientes con cronologías profesionales navegables ("filmografía gastronómica"), evitando el texto libre como identificador de personas.
- **Identidad visual de "museo digital":** un sistema editorial definido (fondo crema `#faf7f2`, titulares grotescos ultra-bold, citas en serif, metadata en monoespaciada y acentos botánicos) que refuerza el peso cultural del archivo.

**Pendiente (captura):** se agregará una imagen del producto más adelante. `<!-- TODO:image:places-app -->`

**Pendiente (repositorio):** se agregará el enlace al repositorio más adelante. `<!-- TODO:repo-link:places-app -->`

**Detalle técnico completo:** [`places-app.md`](./places-app.md)

---

## Convenciones del README

Para que un proyecto nuevo sea consistente, este README sigue una estructura fija:

- **Jerarquía de títulos:** `## Proyectos` agrupa los proyectos; cada proyecto es un `### <Nombre>`.
- **Orden de bloques por proyecto:** (1) *pitch* en una cita, (2) ficha (*tipo*, *alcance*, *estado*), (3) *stack* en una línea con `code spans`, (4) **Decisiones técnicas**, (5) *pendiente* de captura, (6) *pendiente* de repositorio, (7) enlace al brief.
- **Placeholders:** los datos aún no disponibles usan una línea visible `**Pendiente: …**` más un marcador comentado `<!-- TODO:<tipo>:<proyecto> -->`. Los enlaces se pueden localizar luego con `grep "TODO" README.md`.
- **Sin badges externos:** el *stack* se muestra con `code spans` en texto, sin servicios de imágenes externos.
- **Idioma:** el contenido está en español; los nombres de productos y tecnologías se conservan en su forma original.
