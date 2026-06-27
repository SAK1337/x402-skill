# skill-pack Specification

## Purpose
TBD - created by archiving change add-design-foundation-skills. Update Purpose after archive.
## Requirements
### Requirement: Skill Pack Directory Structure
The x402 skill pack SHALL live under a top-level `skills/` directory, with each skill in
its own kebab-case subdirectory containing a `SKILL.md` file as the entry point.

#### Scenario: Skill discovered by Claude Code
- **WHEN** Claude Code loads the project's skills
- **THEN** each `skills/<skill-name>/SKILL.md` is discoverable and invocable by name

#### Scenario: Adding a new skill to the pack
- **WHEN** a contributor adds a new skill to the pack
- **THEN** they create `skills/<new-skill>/SKILL.md` following the shared format
- **AND** no existing skill directory needs to be modified

### Requirement: SKILL.md Frontmatter Format
Every `SKILL.md` SHALL begin with YAML frontmatter containing a `name` field matching its
directory and a `description` field that states when the skill should be used, including
trigger phrases.

#### Scenario: Valid frontmatter authored
- **WHEN** a skill's `SKILL.md` is created
- **THEN** it contains `name` and `description` frontmatter keys
- **AND** the `description` names the situations and phrases that should invoke the skill

#### Scenario: Name matches directory
- **WHEN** a skill named `frontend-design` is authored
- **THEN** its directory is `skills/frontend-design/` and its frontmatter `name` is `frontend-design`

### Requirement: Shared Stack Convention
The skill pack SHALL document a single shared target stack — Next.js, Tailwind CSS, and
shadcn/ui — and implementation-oriented skills SHALL reference it rather than introducing
a different stack.

#### Scenario: Stack referenced consistently
- **WHEN** any implementation-oriented skill needs to name the front-end stack
- **THEN** it references the shared convention (Next.js + Tailwind + shadcn/ui)
- **AND** does not introduce a conflicting framework or styling system

