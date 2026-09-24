## Purpose

Define the portfolio README that serves as the repository's public entry point, presenting each project clearly and surfacing the technical decisions that demonstrate engineering depth.

## Requirements

### Requirement: Single portfolio entry point

The repository SHALL provide a root-level `README.md` written in Spanish that acts as the portfolio landing document. It SHALL be the only top-level entry point; the existing project briefs (`places-app.md`, `postulog.md`, `multimax-crm.md`, `odontosoft.md`) SHALL remain as supporting detail rather than serving as entry points.

#### Scenario: Visitor opens the repository

- **WHEN** a visitor opens the repository landing page
- **THEN** the rendered `README.md` is shown as the portfolio overview, in Spanish

#### Scenario: Briefs are referenced, not duplicated

- **WHEN** the README describes a project
- **THEN** it links to that project's brief file for full detail instead of copying the entire brief inline

### Requirement: Complete and consistent project coverage

The README SHALL present every one of the four projects (Places, PostuLog, Multimax CRM, OdontoSoft) using the same section template, so each project is directly comparable.

#### Scenario: All four projects are present

- **WHEN** a visitor scans the projects section
- **THEN** exactly four project entries appear, one per brief, with no project omitted

#### Scenario: Uniform project structure

- **WHEN** any two project entries are compared
- **THEN** both follow the same heading level and the same ordered subsections (pitch, context, stack, technical decisions, links/images)

### Requirement: Highlighted technical decisions per project

Each project entry SHALL include a dedicated, clearly-labeled **Decisiones técnicas** block containing concrete engineering decisions drawn from that project's brief. Vague marketing statements SHALL NOT substitute for concrete decisions.

#### Scenario: Technical decisions are concrete

- **WHEN** a reviewer reads a project's Decisiones técnicas block
- **THEN** it lists specific, project-grounded decisions (for example, forced tool-use for LLM extraction, soft-delete invariants, RBAC separation, async-by-default architecture) rather than generic claims

#### Scenario: Decisions are attributable to their project

- **WHEN** a decision is listed under a project
- **THEN** that decision is supported by the corresponding brief and not reused verbatim across unrelated projects

### Requirement: Deferred content uses explicit placeholders

Repository links and images are not yet available. The README SHALL represent them with explicit, visibly-marked placeholders and SHALL NOT invent URLs or image paths.

#### Scenario: Missing repository link

- **WHEN** a project's repository URL is not yet known
- **THEN** the README shows a clearly marked placeholder (for example, `<!-- TODO: repo link -->`) instead of a fabricated or guessed URL

#### Scenario: Missing images

- **WHEN** a project has no screenshot or image yet
- **THEN** the README shows a clearly marked image placeholder that indicates where the image will go, without referencing a non-existent file

### Requirement: Navigation and orientation

The README SHALL let a visitor quickly orient and navigate: it SHALL include a short personal header (who the author is and how to make contact) and a table of contents linking to each project section.

#### Scenario: Table of contents resolves

- **WHEN** a visitor uses the table of contents
- **THEN** each link navigates to the matching section heading within the README

#### Scenario: Contact is discoverable

- **WHEN** a visitor wants to reach the author
- **THEN** the README header exposes contact channels without requiring a separate file

### Requirement: Extensible conventions

The README SHALL document or demonstrate the conventions (heading hierarchy, project section template, badge style) used to add future projects, so a new project can be added consistently.

#### Scenario: Adding a fifth project

- **WHEN** a maintainer adds a new project section
- **THEN** the existing structure and conventions make the required shape of that section unambiguous
