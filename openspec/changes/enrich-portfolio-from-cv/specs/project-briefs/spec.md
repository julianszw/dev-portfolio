## Purpose

Define the four per-project brief documents in the repository and the personal-context enrichment each must carry, linking every project to the author's real professional trajectory without fabricating claims.

## ADDED Requirements

### Requirement: One brief per project

The repository SHALL contain one root-level brief document per project: `multimax-crm.md`, `odontosoft.md`, `postulog.md` and `places-app.md`. Each brief SHALL remain the detailed technical source for its project.

#### Scenario: All four briefs exist

- **WHEN** the repository root is inspected
- **THEN** all four brief files are present, one per project

#### Scenario: Briefs keep their technical detail

- **WHEN** a brief is read after enrichment
- **THEN** its existing technical content (stack, modules, decisions) is preserved rather than replaced

### Requirement: Personal context enrichment

Each brief SHALL include a personal-context section that connects the project to the author's real professional trajectory, explaining what the project demonstrates relative to the author's backend, fintech and AI-engineering experience.

#### Scenario: Personal context is present in every brief

- **WHEN** any of the four briefs is opened
- **THEN** it contains a clearly identified personal-context section

#### Scenario: Context is specific, not generic

- **WHEN** a reviewer reads a brief's personal-context section
- **THEN** it relates the project to concrete aspects of the author's real experience or positioning rather than generic self-praise

### Requirement: Uniform placement and structure

The personal-context section SHALL appear at the same position and use the same heading level in every brief, so the four briefs remain directly comparable.

#### Scenario: Consistent placement

- **WHEN** any two briefs are compared
- **THEN** the personal-context section appears at the same structural position and heading level in both

### Requirement: Grounded and non-fabricated context

Personal-context statements in the briefs SHALL be supported by the author's canonical CV source and by the project's own brief content. The enrichment SHALL NOT invent employers, metrics, dates or claims.

#### Scenario: Claims are supported

- **WHEN** a personal-context statement is checked
- **THEN** it is supported by the canonical source or the project brief, with no invented facts

#### Scenario: No fabricated assets

- **WHEN** the enrichment adds links or assets
- **THEN** it adds none beyond those already known, and deferred items remain explicit placeholders
