# x402 Skill Pack — Project Guide

## What this repo is
A **Claude skill pack** for building x402-driven chatbot front ends. It contains reusable
skills under `skills/<name>/SKILL.md` — *not* the chatbot application. Skills are authored
via OpenSpec proposals in `openspec/changes/` and populate `skills/` as they are implemented.

See `README.md` for the skill catalog and `openspec/project.md` for full conventions and
domain context.

## Key facts to respect
- **x402** = payments over the HTTP `402 Payment Required` status: server returns `402` with
  payment requirements → client returns a **signed, gasless stablecoin authorization**
  (EIP-3009, e.g. USDC) in the x402 payment header → a **facilitator** verifies and settles
  it → resource is released with settlement details. Approval is a *signature*, not a manually
  broadcast transaction.
- Treat exact header/field names as defined by the x402 spec and the chosen facilitator —
  do not hard-code one naming scheme (the protocol has version drift). Source of truth:
  https://github.com/x402-foundation/x402 and https://www.x402.org/.
- **Shared app stack** (what skills generate): Next.js + Tailwind CSS + shadcn/ui.

## Conventions
- One skill = one OpenSpec capability; kebab-case `name` matches the directory.
- `skill-pack` owns shared conventions; other skills reference it rather than redefining.
- Later skills compose earlier ones (builder consumes design + payment skills; reviewers last).
- Aim for a serious, trust-forward aesthetic; avoid generic "AI" and flashy "crypto dApp" looks.

## Working here
- Use the OpenSpec workflow: propose → approve → implement → archive.
- Validate before sharing: `openspec validate <change-id> --strict`.

<!-- OPENSPEC:START -->
# OpenSpec Instructions

These instructions are for AI assistants working in this project.

Always open `@/openspec/AGENTS.md` when the request:
- Mentions planning or proposals (words like proposal, spec, change, plan)
- Introduces new capabilities, breaking changes, architecture shifts, or big performance/security work
- Sounds ambiguous and you need the authoritative spec before coding

Use `@/openspec/AGENTS.md` to learn:
- How to create and apply change proposals
- Spec format and conventions
- Project structure and guidelines

Keep this managed block so 'openspec update' can refresh the instructions.

<!-- OPENSPEC:END -->