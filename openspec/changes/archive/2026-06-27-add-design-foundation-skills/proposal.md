# Change: Add x402 Skill Pack Foundation (Design Skills)

## Why
An x402-driven chatbot needs a polished, trustworthy, non-generic UI built around
metered HTTP payments. To build it repeatably we need a reusable Claude skill pack.
This change lays the foundation: the pack structure, shared conventions, and the two
design-thinking skills that every later phase depends on — one for visual direction
and one for chat product UX. Later phases (payment/commerce, builder, review) consume
these specs.

## What Changes
- Establish the top-level `skills/` pack structure and a shared `SKILL.md` format.
- Document the shared target stack: **Next.js + Tailwind CSS + shadcn/ui**.
- Add the **frontend-design** skill (distinctive, production-grade visual direction).
- Add the **chatbot-ui-designer** skill (chat layout, streaming/agent states, product
  pre-coding checklist).
- Populate `openspec/project.md` with x402 chatbot context and conventions (currently
  an empty template).

## Impact
- Affected specs: `skill-pack` (new), `frontend-design` (new), `chatbot-ui-designer` (new)
- Affected code: `skills/` (new directory), `openspec/project.md`
- Dependents: `add-payment-commerce-skills`, `add-implementation-builder-skill`, and
  `add-quality-trust-skills` all build on the conventions established here.
