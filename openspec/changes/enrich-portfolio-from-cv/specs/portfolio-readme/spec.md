## REMOVED Requirements

### Requirement: Single portfolio entry point

**Reason**: The repository no longer ships a root `README.md`; it is removed from tracking and added to `.gitignore`. The portfolio entry point moves to the new personal profile document.
**Migration**: Use the `personal-profile` capability (root `perfil.md`) as the portfolio entry point. Do not recreate `README.md`.

### Requirement: Complete and consistent project coverage

**Reason**: The requirement mandated the README to present the four projects. With the README removed, project presentation is owned by the profile document and the project briefs.
**Migration**: See `personal-profile` (navigation to briefs) and `project-briefs` (per-project documents).

### Requirement: Highlighted technical decisions per project

**Reason**: The dedicated "Decisiones técnicas" block was a README requirement; the README no longer exists.
**Migration**: Project technical decisions remain in each brief under `project-briefs`; the profile links to those briefs.

### Requirement: Deferred content uses explicit placeholders

**Reason**: The placeholder requirement applied to the README's deferred repository links and images. The README is removed.
**Migration**: Keep deferred links and images as explicit placeholders inside the project briefs, per `project-briefs`.

### Requirement: Navigation and orientation

**Reason**: README-based navigation (personal header plus table of contents) is retired with the README.
**Migration**: Navigation is provided by the `personal-profile` document, which introduces the author and links every brief.

### Requirement: Extensible conventions

**Reason**: The README conventions existed to add README project sections consistently; that document is retired.
**Migration**: Conventions for adding a new project now live in the `project-briefs` capability (uniform structure and placement).
