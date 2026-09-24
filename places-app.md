# Places — El Letterboxd de la Gastronomía & Archivo Culinario

> **Propósito del Repositorio (Portfolio):** Este repositorio contiene la implementación completa de **Places**, una plataforma documental y museo digital diseñada para la crítica, preservación y memoria cultural gastronómica, inspirada en la arquitectura social y de coleccionismo de *Letterboxd*.

---

## 1. Filosofía de Producto (No Negociable)

Places **no es un TripAdvisor**. Su ADN conceptual se rige por cuatro pilares inmutables:
1. **Inmutabilidad Histórica:** Ningún establecimiento se borra jamás, ni siquiera cuando cierra definitivamente. El estado del local pasa a `closed` (con marca temporal de cierre), pero la ficha permanece 100% navegable, citable y calificable retrospectivamente en la bitácora histórica.
2. **Peso Cultural y Crítico en Calificaciones:** Sistema de valoración ponderada de 0.5 a 5.0 estrellas, estructurado con rigor crítico, reseñas detalladas y metadatos de atmósfera/tags.
3. **Entidad Crew (Dirección & Reparto):** Chefs, bartenders, pasteleros y sommeliers poseen entidades de persona (`Person`) independientes con cronologías profesionales navegables ("filmografía gastronómica").
4. **Protección de Datos & Cero Hard Deletes:** Prohibición absoluta de sentencias `DELETE` físico sobre entidades cardinales (`Venue`, `Log`, `Review`, `Person`, `Event`). Las bajas se gestionan mediante borrado lógico (soft-delete) auditado.

---

## 2. Stack Tecnológico

- **Backend:** Python 3.12 + FastAPI (Async) + SQLAlchemy 2.0 + Alembic (Gestión de migraciones).
- **Base de Datos:** PostgreSQL con extensión **pgvector** para embeddings de reseñas y búsqueda semántica (con soporte de desarrollo transparente a SQLite).
- **Frontend:** Next.js 14 (App Router) + TypeScript + Tailwind CSS + Lucide Icons.
- **Identidad Visual (Estética Editorial de Museo Digital):**
  - **Fondo base:** Crema editorial (`#faf7f2`).
  - **Tipografías:** Titulares en Grotesco ultra-bold (*Archivo Black* / *Anton*), Subtítulos y citas en *Playfair Display*, Metadata y tags en *Space Mono*.
  - **Acentos:** Tonos Sage / Botánicos (`#395d43` a `#4d7c5b`).

---

## 3. Arquitectura de Datos & Modelos Principales

- `Venue`: Establecimiento gastronómico, almacena estado (`active`, `closed`), dirección, coordenadas, valoración media y tags culturales.
- `Person`: Profesionales de la gastronomía (chefs, sommeliers, etc.).
- `VenueCrewRole`: Relación asociativa que vincula personas a establecimientos con roles específicos y períodos de actividad.
- `Log` / `Review`: Bitácora o registro de visitas de los usuarios con puntuación por estrellas, fecha de consumo y texto de reseña.
- `WantToGo`: Lista de deseos o establecimientos pendientes por visitar de cada usuario.
- `List`: Colecciones curadas de lugares creadas por la comunidad.
- `Event`: Pop-ups, takeovers, cenas maridaje y eventos efímeros.
- `Taxonomy`: Categorización flexible mediante tags, vibes (atmósferas) y tipos de cocina.

---

## 4. Estructura del Código

```text
├── backend/
│   ├── alembic/              # Migraciones de base de datos
│   ├── app/
│   │   ├── core/             # Configuración y conexión DB (con soporte vector)
│   │   ├── models/           # Modelos ORM SQLAlchemy 2.0 (Venue, Person, Log, etc.)
│   │   ├── schemas/          # Validación y serialización con Pydantic v2
│   │   ├── api/v1/           # Endpoints REST (venues, crew, logs, search, etc.)
│   │   └── ml/               # Embeddings y recomendación semántica (pgvector / similitud coseno)
│   ├── scripts/seed/         # Scripts de población y curación de datos iniciales
│   └── tests/                # Pruebas unitarias de invariantes (soft-deletes, inmutabilidad, etc.)
└── frontend/
    ├── app/                  # Next.js App Router (Directorios: /venues, /feed, /crew, /lists, /want-to-go, /events)
    ├── components/           # Componentes UI reutilizables (AppShell, VenueCard, RatingStars, LogModal)
    └── lib/                  # Clientes de API y utilidades de red
```

---

## 5. Guía de Arranque Rápido para la IA (Nuevo Repositorio Portfolio)

Instrucciones para desplegar o inicializar el proyecto en tu nuevo repositorio de portfolio en GitHub:

1. **Configurar el Backend:**
   ```bash
   cd backend
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt
   alembic -c alembic.ini upgrade head
   python scripts/seed/seed_data.py
   python scripts/seed/seed_more.py
   uvicorn backend.app.main:app --reload --port 8000
   ```

2. **Configurar el Frontend:**
   ```bash
   cd frontend
   npm install
   npm run dev
   ```

---

## Contexto profesional

**Rol en el portfolio:** plataforma documental full-stack con backend Python/FastAPI y frontend Next.js, orientada a datos y experiencia de usuario.

**Conexión con mi trayectoria:** las invariantes de "cero hard deletes" y soft-delete auditado son análogas al rigor de integridad y consistencia (ACID) que aplico en sistemas financieros. La búsqueda semántica con pgvector conecta con mi línea de AI Engineering (bases de datos vectoriales), y el modelado de entidades como `Person` y `VenueCrewRole` refleja el modelado relacional y de dominio que practico.

**Qué demuestra:** modelado de dominio rico con invariantes explícitas e integración de capacidades de datos/IA sobre una base backend sólida en Python.
