## Why

The repository's `README.md` was generated with placeholder identity/contact, a generic "about me" and TODO markers. The author's real professional data already exists as a canonical source in the local `mi-cv` project. The portfolio should stop shipping the generated README and instead present a real personal profile document derived from that canonical data, with the four project briefs connected to the author's actual backend/fintech/AI trajectory.

## What Changes

- Remove root `README.md` from the repository and add it to `.gitignore` (untrack it). **BREAKING** for the repository landing: GitHub will no longer render a README, so the portfolio entry point moves to the personal profile document.
- Add a new root personal profile markdown (`perfil.md`, Spanish) containing real identity, contact channels, professional experience, education, skills and languages derived from the canonical CV source (`mi-cv`). It replaces the placeholder "Sobre mí" content and becomes the always-available reference about the author.
- Enrich the four existing project briefs (`multimax-crm.md`, `odontosoft.md`, `postulog.md`, `places-app.md`) with personal context linking each project to the author's real backend/fintech/AI experience and role.
- Provide navigation from the profile document to the four project briefs, replacing the table of contents that the removed README used to own.

## Capabilities

### New Capabilities
- `personal-profile`: the root personal profile markdown that serves as the portfolio entry point and always-available reference about the author — identity, contact, experience, education, skills, languages — with honesty/no-fabrication rules and navigation to the project briefs.
- `project-briefs`: the per-project brief documents and the personal-context enrichment they must carry, connecting each project to the author's real trajectory without fabricating claims.

### Modified Capabilities
- `portfolio-readme`: the README entry-point capability is retired. `README.md` is removed and gitignored; its presentation requirements (entry point, project coverage, technical decisions, placeholders, navigation, conventions) transfer to `personal-profile` and `project-briefs`.

## Impact

- Deleted: root `README.md` (removed from git tracking; added to `.gitignore`).
- New: `.gitignore` (if absent), root `perfil.md`.
- Modified: `multimax-crm.md`, `odontosoft.md`, `postulog.md`, `places-app.md`.
- Main spec `openspec/specs/portfolio-readme/spec.md` loses its requirements (capability retired).
- Documentation-only change: no runtime, API, dependency or build impact.
- Consequence: the repository will have no rendered GitHub README landing page; the profile markdown is a plain file and is not auto-rendered by GitHub as the repo front page.
