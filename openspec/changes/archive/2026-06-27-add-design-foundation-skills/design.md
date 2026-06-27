## Context
We are building a skill pack (not the app itself) that lets Claude reliably generate an
x402-driven chatbot front end. The work spans four concerns the user wants kept separate:
visual design, chat product UX, payment-flow UX, and protocol/implementation. This change
covers the first two plus the pack scaffolding that all four share.

## Goals / Non-Goals
- Goals:
  - A discoverable `skills/` pack with a consistent `SKILL.md` format.
  - One shared, authoritative stack convention so later skills don't diverge.
  - Design skills that bias Claude toward distinctive, trustworthy UI.
- Non-Goals:
  - Building the chatbot application (that consumes these skills later).
  - Implementing x402 payment logic or wallet integration (covered by later phases).

## Decisions
- **Decision: One skill = one OpenSpec capability.** Skills are single-purpose and
  self-contained, which matches OpenSpec's capability model and keeps specs reviewable.
- **Decision: Phase the pack into 4 changes by build order** (design → payment/commerce →
  builder → review). This mirrors dependency direction: the builder consumes design and
  payment specs; reviewers run last.
- **Decision: Skills are Claude Code skills** — plain folders with a `SKILL.md` entry file
  and YAML frontmatter (`name`, `description`) whose description drives invocation.
- Alternatives considered: one proposal per skill (9 folders — more overhead, weaker
  narrative) and a single monolithic proposal (hard to review, no natural approval gates).

## Risks / Trade-offs
- Risk: skills drift on stack/conventions over time → Mitigation: `skill-pack` capability
  owns the shared conventions; other skills reference it instead of redefining.
- Risk: design skills are subjective and hard to verify → Mitigation: specs assert the
  presence of concrete guidance (named states, checklists, anti-patterns), not taste.

## Migration Plan
Greenfield — no existing skills or app. Phases can be implemented and approved
independently in build order.

## Open Questions
- None blocking. Wallet/protocol library choices are deferred to the relevant later phase.
