## Context

See `proposal.md` — Why. Constraints that shape this design:

- The repository is documentation-only (Markdown). There is no build, runtime, test harness or CI.
- The author's canonical professional data lives in a separate local project (`mi-cv`): `fuentes/base-profile/master-profile.md`, `fuentes/base-profile/contact.md`, `docs/INSIGHTS.md` and `docs/skills-selection.md` are the authoritative sources.
- The current root `README.md` is git-tracked (commit `82162b5`) and contains placeholders (`TODO`) plus generic "about me" text.
- The four briefs mix Spanish and English and each ends with an "instructions for the AI" section. Enrichment must not destroy their existing technical detail.
- Requirement specs for this change: `specs/personal-profile/spec.md`, `specs/project-briefs/spec.md`, `specs/portfolio-readme/spec.md`.

## Goals / Non-Goals

**Goals:**

- Establish `perfil.md` as the single, real source of personal presentation and the navigation entry point.
- Remove and gitignore `README.md` cleanly (including untracking it in git).
- Add a uniform, grounded personal-context section to each of the four briefs.
- Keep all content traceable to `mi-cv`; invent nothing.

**Non-Goals:**

- Not building a website, theme or GitHub Pages site.
- Not copying the full CV or all `mi-cv` content into the portfolio; only relevant, public-safe information.
- Not modifying or publishing anything inside `mi-cv`.
- Not creating repository links, screenshots or metrics that do not exist.

## Decisions

### Decision: Profile file name and language

Use `perfil.md` at the repository root, written in Spanish, matching the portfolio's content language and the author's market (ARG). Rejected: `README.md` (README is being removed), `about.md`/`profile.md` (English filenames inconsistent with the Spanish content and the author's primary market).

### Decision: Derive content read-only from `mi-cv`; never link the local path

Content is extracted from the canonical sources during implementation and written into `perfil.md` as plain Markdown. The public file references no local filesystem path and does not embed or clone the CV. Rejected: linking to `mi-cv` (private/local, not portable); copying entire CV sections (duplication and drift).

### Decision: Contact channels shown publicly

Include email, GitHub, LinkedIn and website (all professional channels from `contact.md`). Exclude the personal phone number and WhatsApp link by default (privacy), as a deliberate, easily reversible choice. Rejected: mirroring every field from `contact.md`, which would expose personal phone data on a public repository.

### Decision: README removal mechanics

Add a root `.gitignore` containing `README.md`, then `git rm --cached README.md` (a tracked file is not ignored until untracked) and delete the working-tree file. Rejected: only deleting the file (it would remain tracked and could be re-added) or only editing `.gitignore` (has no effect on an already-tracked file).

### Decision: Enrichment section appended uniformly to every brief

Append one final section titled `## Contexto profesional` to each brief, after the existing content, in Spanish. It links the project to concrete aspects of the author's real trajectory (backend, fintech, AI engineering) supported by the canonical source. Rejected: interleaving personal context into existing sections (would disturb the imported technical detail and vary by brief) and placing it at the top (would push the project's own content down and differ per file layout).

### Decision: Profile becomes the navigation hub

`perfil.md` carries a short table of contents linking to `multimax-crm.md`, `odontosoft.md`, `postulog.md` and `places-app.md`, replacing the README's navigation. Rejected: leaving navigation only inside the briefs (no single entry point after README removal).

### Decision: Retire the `portfolio-readme` capability, delegate to new capabilities

The README-based requirements are removed from `portfolio-readme` and reintroduced, retargeted to `perfil.md`/briefs, under `personal-profile` and `project-briefs`. Rejected: silently leaving a main spec that asserts a README the repository must not have.

## Risks / Trade-offs

- [GitHub will stop rendering a repository README landing page] → Explicit and accepted by the user; `perfil.md` is the entry point. If a rendered landing page is wanted later, it can be reintroduced as a separate change.
- [`mi-cv` facts may drift from the profile over time] → Profile is a snapshot; provenance recorded in this change, and future sync is a normal follow-up change.
- [Untracked README may still exist locally and confuse visitors] → Implementation deletes the working-tree file in addition to untracking it.
- [Briefs mix languages; adding Spanish sections could read inconsistently] → The enrichment section is clearly delimited and Spanish, consistent with the profile and an acceptable, documented trade-off.
- [Risk of overstating skills in a public doc] → Only source-supported skills; conditional skills (frontend) kept conditional, per spec.

## Migration Plan

1. Create `.gitignore` with `README.md`.
2. `git rm --cached README.md` and delete the file from the working tree.
3. Create `perfil.md` from the canonical `mi-cv` sources.
4. Append `## Contexto profesional` to each brief.
5. Verify specs' scenarios; rollback is a plain `git checkout` of the affected files since no external state changes.

## Open Questions

- Whether to also publish phone/WhatsApp (default: excluded). Deferrable; adding a line later does not change the specs.
