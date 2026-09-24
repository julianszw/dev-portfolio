## Context

See `proposal.md` for motivation. Constraints that shape this design:

- The repository's only deliverables are Markdown documents. There is no build, runtime, or test harness.
- Four project briefs already exist and are the authoritative source for each project's stack, modules, and technical decisions. The design must not depend on information beyond them.
- Repository URLs and images are explicitly deferred by the user ("más adelante, agregaremos links"; "me encargaré de enriquecer con imágenes"). The README must be complete-looking now while marking those gaps honestly.
- Content language is Spanish; project briefs are in Spanish and English.

## Goals / Non-Goals

**Goals:**

- Produce one scannable root `README.md` that presents all four projects consistently.
- Make each project's engineering depth legible via concrete **Decisiones técnicas**.
- Keep all deferred content as explicit, non-fabricated placeholders.
- Establish a project-section template so a fifth project can be added later without rework.

**Non-Goals:**

- Not a website or app; no framework, build step, or deployment configuration.
- Not a rewrite of the four briefs; they remain the detailed source documents.
- Not fabricating repository links, screenshots, metrics, or dates.
- Not translating the briefs.

## Decisions

### Decision: Root `README.md` as the single entry point; briefs stay in place

The portfolio lives at `README.md` in the repository root. The four briefs remain untouched as backing docs and are linked as "detalle técnico completo".

- **Rationale:** GitHub renders root `README.md` automatically; keeping briefs avoids losing the raw source and keeps the README short.
- **Alternatives considered:** (a) converting each brief into README sections — rejected as duplication and maintenance burden; (b) a `docs/` folder of generated pages — rejected as unnecessary for a Markdown-only deliverable.

### Decision: Fixed project-section template

Every project uses the same ordered subsections:

1. `### <Proyecto> — <pitch de una línea>`
2. Ficha corta (rol, tipo de producto, estado) as a small table or bold labels
3. Stack en una línea (backend / frontend / datos / infra)
4. **Decisiones técnicas** — 3 a 5 bullets, formato `**Decisión:** por qué / trade-off`
5. Placeholder de captura
6. Placeholder de enlace al repositorio
7. Enlace al brief detallado

- **Rationale:** Identical shape makes projects comparable and makes later edits mechanical; satisfies the "uniform project structure" requirement.
- **Alternatives considered:** free-form narrative per project — rejected because it hurts scannability and consistency.

### Decision: Project order by end-to-end breadth

Order projects by how much of the stack each demonstrates end to end: **Multimax CRM → OdontoSoft → PostuLog → Places** (operational product with infra → clinical SaaS → AI/LLM pipeline → consumer platform with ML/vector search). This is a presentation choice, not a ranking.

- **Rationale:** Leads with concrete shipped-style systems; ordering is explicit so it can be reordered deliberately.
- **Alternatives considered:** alphabetical or brief-file order — rejected as arbitrary.

### Decision: Visible placeholders, not hidden HTML comments

Deferred items use a visible line plus a searchable marker, e.g.:

```markdown
> 🧩 **Pendiente:** enlace al repositorio <!-- TODO:repo-link:multimax-crm -->
```

and

```markdown
> 🖼️ **Pendiente:** captura de pantalla <!-- TODO:image:multimax-crm -->
```

- **Rationale:** HTML comments alone are invisible on GitHub, so the gap would look like an omission. The comment marker makes `TODO:` greppable so the user can find every gap later.
- **Alternatives considered:** bare HTML comments — rejected (invisible); fake URLs — rejected (dishonest, violates a spec requirement).

### Decision: Technical decisions traced to briefs

Each project's **Decisiones técnicas** bullets are derived from its brief and must be concrete. Source mapping to use during implementation:

- **Multimax CRM:** FSM inbound WhatsApp bot, BullMQ + Redis rate-limiting/jitter, SQLite→PostgreSQL + Docker Compose scaling path, JWT + RBAC, AI PDF/image catalog extraction.
- **OdontoSoft:** multi-resource drag & drop agenda with conflict validation, RBAC separation (clinical vs administrative), FDI odontogram, immutable appointment state machine (`historialEstados`), dual mock/http repository abstraction, Zustand modular stores.
- **PostuLog:** async-by-default I/O, forced Pydantic tool-use for extraction, UUID + JSONB persistence, layered router→service→model architecture, `trafilatura` content cleaning, pytest + respx.
- **Places:** no hard deletes / soft-delete invariants for cardinal entities, pgvector semantic search with SQLite dev fallback, weighted critical rating, `Person`/`VenueCrewRole` professional timelines, editorial "digital museum" design system.

- **Rationale:** Grounds the README in verifiable facts from the briefs and directly satisfies "en cada proyecto se destaquen decisiones técnicas".
- **Alternatives considered:** generic per-project strengths — rejected as non-specific.

### Decision: Self-contained enrichment; no external badge services

Stack is shown as inline code spans / bold labels rather than shields.io badge images.

- **Rationale:** No external image dependency, renders offline and in any Markdown viewer, and avoids conflating volunteer badge images with the user's planned screenshots.
- **Alternatives considered:** shields.io badges — deferred as an optional later enhancement, not a blocker.

## Risks / Trade-offs

- [Briefs contain aspirational or unverifiable claims] → Only assert what the brief states; phrase as designed/implemented per brief, and keep the brief link for provenance.
- [README grows long and becomes unscannable] → Keep each project to a tight template, one-line stack, and 3–5 decision bullets; push detail to briefs via links.
- [Placeholders look unfinished] → Mark them explicitly as intentionally pending for links/images the user will add; this is the requested workflow, not an omission.
- [Project order is opinionated] → Ordering is a documented decision and trivially reorderable; sections are independent.
- [Language drift between Spanish README and English briefs] → Write the README in Spanish and preserve exact product/tech names in their original form.

## Open Questions

- Exact repository URLs and screenshot assets — deferred by the user; placeholders cover them.
- Final project order — documented default above; can be reordered without changing any spec.
