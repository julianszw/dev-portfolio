## Purpose

Define the repository's root personal profile markdown that serves as the portfolio entry point and the always-available reference about the author, presenting real identity, contact, trajectory, education, skills and languages drawn from the author's canonical CV source.

## ADDED Requirements

### Requirement: Personal profile as the portfolio entry point

The repository SHALL provide a root-level `perfil.md` written in Spanish that acts as the portfolio landing document and the navigation entry point to the project briefs. The root `README.md` SHALL be removed from the repository and SHALL be listed in `.gitignore`; no root-level `README.md` SHALL be present.

#### Scenario: Profile document is present

- **WHEN** a visitor opens the repository root
- **THEN** a `perfil.md` file is present and is the document that introduces the author and links the projects

#### Scenario: README is removed and ignored

- **WHEN** the repository is inspected after the change
- **THEN** `README.md` no longer exists in the tracked files and `README.md` is listed in `.gitignore`

### Requirement: Real identity and contact channels

The profile SHALL present the author's real name and role, and SHALL expose professional contact channels (for example email, GitHub, LinkedIn, website). Placeholder markers such as `TODO`, `Pendiente` or "nombre aquí" SHALL NOT remain in the profile.

#### Scenario: Identity is present

- **WHEN** a visitor reads the top of the profile
- **THEN** the author's name and professional role are stated explicitly

#### Scenario: Contact is discoverable

- **WHEN** a visitor wants to reach the author
- **THEN** the profile exposes at least one professional contact channel without requiring a separate file

#### Scenario: No placeholders remain

- **WHEN** the profile is searched for placeholder markers
- **THEN** no unfinished placeholder text remains

### Requirement: Professional trajectory

The profile SHALL summarize the author's real professional experience, including each employer, role and date range, and the concrete technical contributions of each position as recorded in the canonical source.

#### Scenario: Experience entries are complete

- **WHEN** a reviewer reads the experience section
- **THEN** each entry names the employer, the role, the date range, and at least one concrete technical contribution

### Requirement: Education and languages

The profile SHALL state the author's formal education and declared language levels.

#### Scenario: Education and languages are present

- **WHEN** a reviewer reads the profile
- **THEN** the formal education (institution, program, dates) and the language levels are stated

### Requirement: Skills grounded in the canonical source

The profile SHALL list the author's technologies, architecture practices and tools consistently with the canonical CV source. It SHALL NOT claim skills, certifications or experience that the source does not support.

#### Scenario: Skills match the source

- **WHEN** any skill listed in the profile is compared with the canonical source
- **THEN** the skill is supported by the source and no unsupported skill is asserted

#### Scenario: Conditional skills are not overstated

- **WHEN** a skill is classified as conditional in the source (for example frontend frameworks)
- **THEN** the profile does not present it as a core, unrestricted competency

### Requirement: Navigation to project briefs

The profile SHALL include navigation links to every project brief so the portfolio can be traversed from the profile document.

#### Scenario: Navigation resolves

- **WHEN** a visitor follows the profile's project navigation
- **THEN** each link targets an existing project brief file in the repository

### Requirement: Honesty and provenance

All personal data in the profile SHALL be derived from the author's canonical CV source. The profile SHALL NOT fabricate URLs, employers, dates, metrics or assets, and SHALL NOT reference the local filesystem path of the canonical source.

#### Scenario: No fabricated data

- **WHEN** a reviewer inspects links, employers, dates and metrics in the profile
- **THEN** each is traceable to the canonical source and none is invented or guessed

#### Scenario: No local path leaked

- **WHEN** the profile is searched for filesystem paths
- **THEN** it contains no absolute local path to the canonical source repository
