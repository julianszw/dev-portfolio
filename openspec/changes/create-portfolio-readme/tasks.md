## 1. README Scaffold

- [x] 1.1 Create root `README.md` with a personal header (nombre, pitch de una línea, canales de contacto) and verify the file exists at the repository root
- [x] 1.2 Add a tabla de contenidos linking to each project section and verify every link anchor matches an existing heading
- [x] 1.3 Add a short "Sobre mí / Stack" section summarizing the technologies across the four projects and verify it renders as a distinct section

## 2. Project Sections

- [x] 2.1 Add the Multimax CRM section using the fixed template (ficha, stack en una línea, **Decisiones técnicas**, placeholders, enlace al brief) and verify it contains 3–5 concrete decisions
- [x] 2.2 Add the OdontoSoft section using the same template and verify it contains 3–5 concrete decisions
- [x] 2.3 Add the PostuLog section using the same template and verify it contains 3–5 concrete decisions
- [x] 2.4 Add the Places section using the same template and verify it contains 3–5 concrete decisions
- [x] 2.5 Verify all four project sections are present, share the same subsection order and heading level, and that no technical decision is duplicated across unrelated projects

## 3. Deferred Content Placeholders

- [x] 3.1 Add one visible repository-link placeholder per project with a `<!-- TODO:repo-link:<project> -->` marker and verify `grep -c "TODO:repo-link" README.md` returns 4
- [x] 3.2 Add one visible image placeholder per project with a `<!-- TODO:image:<project> -->` marker and verify `grep -c "TODO:image" README.md` returns 4
- [x] 3.3 Add a link from each project section to its brief file and verify all four linked files exist (for example with `ls`)

## 4. Consistency and Honesty Pass

- [x] 4.1 Verify the README introduces no fabricated URLs or assets: inspect every link and confirm none point to an invented repo or missing image
- [x] 4.2 Verify the README is written in Spanish while preserving product and technology names verbatim
- [x] 4.3 Confirm the conventions (heading hierarchy and project template) are evident enough that a fifth project can be added consistently, or add a short note documenting them

## 5. Final Verification

- [x] 5.1 Trace each project's **Decisiones técnicas** back to its brief and verify every bullet is supported by the source document
- [x] 5.2 Verify `README.md` satisfies every scenario in `specs/portfolio-readme/spec.md` and run `openspec validate create-portfolio-readme`
