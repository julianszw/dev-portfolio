## 1. Remove and gitignore the GitHub README

- [x] 1.1 Create a root `.gitignore` containing `README.md` and verify the entry is present (`grep -n '^README.md$' .gitignore`)
- [x] 1.2 Untrack the README with `git rm --cached README.md` and delete the working-tree file, then verify `README.md` no longer exists and does not appear in `git ls-files`
- [x] 1.3 Verify `git status` shows `README.md` neither as tracked nor as a new untracked file (ignored), confirming removal plus ignore works together

## 2. Create the personal profile

- [x] 2.1 Create root `perfil.md` in Spanish with a header containing the real name, professional role and a one-line positioning derived from the canonical CV source, and verify no `TODO`/`Pendiente` placeholder remains
- [x] 2.2 Add a contact block with email, GitHub, LinkedIn and website from the canonical contact source (excluding phone/WhatsApp) and verify each link matches the source exactly
- [x] 2.3 Add a professional-experience section with employer, role, date range and concrete contributions for each position from the canonical source, and verify every entry names employer, role, dates and at least one contribution
- [x] 2.4 Add education and languages sections from the canonical source and verify institution/program/dates and language levels are stated
- [x] 2.5 Add a skills section consistent with the canonical skills inventory, keeping conditional skills (frontend) clearly non-core, and verify no unsupported skill is claimed
- [x] 2.6 Add a table of contents linking to `multimax-crm.md`, `odontosoft.md`, `postulog.md` and `places-app.md`, and verify all four target files exist
- [x] 2.7 Verify `perfil.md` contains no absolute filesystem path (for example `grep -n '/home/' perfil.md` returns nothing)

## 3. Enrich the project briefs with personal context

- [x] 3.1 Append a `## Contexto profesional` section to `multimax-crm.md` connecting it to the author's real backend/fintech/AI trajectory, and verify it is supported by the canonical source and the brief
- [x] 3.2 Append the same `## Contexto profesional` section to `odontosoft.md` following the uniform placement and verify the existing technical content is unchanged
- [x] 3.3 Append the same `## Contexto profesional` section to `postulog.md` following the uniform placement and verify the existing technical content is unchanged
- [x] 3.4 Append the same `## Contexto profesional` section to `places-app.md` following the uniform placement and verify the existing technical content is unchanged
- [x] 3.5 Verify all four briefs contain `## Contexto profesional` at the same structural position and heading level, and that no employer, metric, date or asset was invented

## 4. Final verification

- [x] 4.1 Verify `perfil.md` satisfies every scenario in `specs/personal-profile/spec.md` (entry point, identity/contact, trajectory, education/languages, grounded skills, navigation, honesty)
- [x] 4.2 Verify the four briefs satisfy every scenario in `specs/project-briefs/spec.md` (one brief per project, personal context, uniform structure, grounded context)
- [x] 4.3 Run `openspec validate enrich-portfolio-from-cv` and confirm the change validates without error
