# PostuLog — Intelligent Job Application CRM & LLM Extraction Engine

> **Portfolio Project Overview & AI Generation Context**
> Este documento contiene toda la arquitectura, especificaciones técnicas, decisiones de diseño y convenciones de código necesarias para que una IA reconstruya, mantenga o entienda completamente el proyecto **PostuLog**.

---

## 🚀 1. Resumen Ejecutivo y Propósito

**PostuLog** es un CRM personal avanzado para el seguimiento de postulaciones laborales que integra **extracción automatizada de ofertas de empleo mediante LLM (DeepSeek / Anthropic)** con **tool calling forzado**, un pipeline Kanban de seguimiento, directorio CRM de empresas y contactos, gestión de entrevistas, tareas y generación automática de cartas de presentación.

Diseñado con una arquitectura limpia en Python 3.12+ (FastAPI) y un frontend moderno (React + Vite + Tailwind + TypeScript), PostuLog demuestra el desarrollo full-stack robusto bajo la metodología **Spec-Driven Development (OpenSpec)**.

---

## 🏗️ 2. Arquitectura de Software y Stack Tecnológico

### Backend (Python / FastAPI)
- **Framework**: FastAPI (asíncrono por completo).
- **Base de Datos & ORM**: PostgreSQL con SQLAlchemy 2.0 (async session, UUID primary keys, JSONB para historial de auditoría y estados).
- **Migraciones**: Alembic.
- **Extracción & Scraping**: `httpx` (async HTTP client), `trafilatura` (limpieza de contenido web descartando ruido, menús y ads), y cliente LLM con **Pydantic Tool Use forzado** para garantizar schemas estructurados y deterministas.
- **Validación**: Pydantic v2.
- **Linter / Formatter**: Ruff.

### Frontend (React / Vite)
- **Framework**: React + Vite + TypeScript.
- **Estilos**: Tailwind CSS (con soporte para tema oscuro/claro).
- **Componentes & UI**: Vistas Kanban (Drag & Drop), Tablas dinámicas, Overlays de detalle, Reportes analíticos y CRM Directory con sincronización automática de empresas.

---

## 📂 3. Estructura de Directorios del Proyecto

```text
postulog/
├── app/
│   ├── main.py                # FastAPI entry point & CORS
│   ├── config.py              # Pydantic BaseSettings (env vars)
│   ├── db.py                  # SQLAlchemy async engine & session factory
│   ├── exceptions.py          # Excepciones de dominio mapeadas a HTTP
│   ├── models/                # Modelos SQLAlchemy 2.0 (Application, Company, Contact, Interview, Task, UserProfile)
│   ├── schemas/               # DTOs Pydantic (request/response y extraction schemas)
│   ├── services/              # Lógica de negocio pura (extractores, CRM, cover letters, pipeline)
│   └── routers/               # Endpoints REST (routers por dominio)
├── migrations/                # Migraciones de Alembic
├── frontend/                  # Aplicación React + Vite + Tailwind
├── openspec/                  # Especificaciones OpenSpec y Change Proposals
├── memory/                    # Memoria persistente del proyecto (decisiones, patterns, learnings)
├── tests/                     # Test suite async con pytest y respx (mocks HTTP)
└── AGENTS.md                  # Guías y roles de agentes especializados
```

---

## 🧠 4. Decisiones Arquitectónicas Clave (Key Decisions)

1. **Async por Defecto**: Todas las operaciones de I/O (llamadas HTTP, consultas a base de datos PostgreSQL, invocaciones al LLM) son estrictamente asíncronas (`async def`, `httpx.AsyncClient`, SQLAlchemy async).
2. **Tool Use Forzado para Extracción**: La extracción de postings desde URLs o texto crudo nunca confía en parsing de texto plano libre; utiliza *Function Calling / Tool Use* con schemas Pydantic estrictos para retornar datos limpios y tipados (título, empresa, salario, modalidad, seniority, etc.).
3. **Persistencia Híbrida y Robusta**: PostgreSQL desde el día uno, utilizando `UUID` como claves primarias y campos `JSONB` para almacenar metadatos flexibles e historiales de cambios de estado.
4. **Arquitectura en Capas Limpia**:
   - `routers/`: Únicamente reciben solicitudes HTTP, validan con DTOs de Pydantic, llaman a servicios y traducen excepciones de dominio a `HTTPException`.
   - `services/`: Contienen toda la lógica de negocio y lanzan excepciones de dominio declaradas en `app/exceptions.py`.
   - `models/`: Definición de tablas relacionales.

---

## 🔌 5. Endpoints y Capacidades Principales del Backend

- `POST /api/v1/extract`: Extrae datos estructurados de una URL de empleo mediante scraping con `trafilatura` + LLM Tool Use.
- `POST /api/v1/extract-text`: Extrae datos estructurados directamente a partir de texto plano pegado por el usuario.
- CRUD Completo de Postulaciones (`/api/v1/applications`): Gestión de estados, filtrado, paginación, notas y detección de duplicados.
- CRM Directory (`/api/v1/companies`, `/api/v1/contacts`): Gestión de empresas asociadas y contactos clave con sincronización automática y enriquecimiento.
- Entrevistas y Tareas (`/api/v1/interviews`, `/api/v1/tasks`): Seguimiento de rondas de entrevistas y pendientes asociados a procesos de selección.
- Generación de Cartas de Presentación (`/api/v1/cover-letters`): Redacción automatizada personalizada al perfil del usuario y la oferta laboral.

---

## 🧪 6. Testing y Calidad

- **Test Framework**: `pytest` + `pytest-asyncio` + `respx` (para mockear peticiones HTTP externas a portales de empleo o APIs de LLM).
- **Linters**: `ruff check` y `ruff format`.

---

## 🤖 7. Instrucciones para la IA Generadora (Prompt para Opencode / Claude / GPT)

Si utilizas este documento para inicializar o clonar el proyecto en un nuevo repositorio portfolio, la IA debe seguir estas directrices:
- Mantener estrictamente la separación de capas (Router ➔ Service ➔ Model/Schema).
- Todo nuevo flujo de datos debe especificarse primero bajo la metodología OpenSpec en `openspec/`.
- Garantizar que cualquier consumo de API externa de LLM utilice validación estricta con Pydantic.
- Preservar la nomenclatura en inglés para código, base de datos y esquemas, manteniendo la documentación de negocio orientada en español/inglés según corresponda.
