# component-polish-reviewer Specification

## Purpose
TBD - created by archiving change add-quality-trust-skills. Update Purpose after archive.
## Requirements
### Requirement: Component Polish Reviewer Skill
The pack SHALL provide a `component-polish-reviewer` skill that performs a final refinement
pass over spacing, visual hierarchy, hover/interaction states, responsive behavior, and
microcopy.

#### Scenario: Polish pass requested
- **WHEN** a user asks Claude for a final polish pass on the chatbot UI
- **THEN** the skill reviews spacing, hierarchy, hover/interaction states, responsive behavior, and microcopy
- **AND** proposes specific refinements

#### Scenario: Refinement over rebuild
- **WHEN** the skill finds issues
- **THEN** it recommends targeted refinements that preserve existing functionality rather than redesigning from scratch

