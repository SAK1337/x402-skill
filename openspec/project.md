# Project Context

## Purpose
This repository is a **Claude skill pack** for building x402-driven chatbot front ends.
It does not contain the chatbot application itself — it contains reusable Claude Code
skills (under `skills/`) that guide Claude to design, build, and review a polished,
trustworthy chatbot UI around x402 metered HTTP payments.

x402 is an open protocol built on the HTTP `402 Payment Required` status code: a server
returns `402` with machine-readable payment requirements, the client returns a signed,
gasless stablecoin payment authorization (e.g. EIP-3009 `transferWithAuthorization`, signed
as an EIP-712 typed-data message, over USDC) in the x402 payment header, and a facilitator
verifies and settles it before the resource is released. EIP-3009 over a stablecoin is the
protocol's primary **`exact`** scheme — the scope this pack targets — not the whole protocol:
x402 is scheme-extensible (e.g. `exact`, `upto`) and is broadening toward other rails, so
skills describe the stablecoin exact-scheme flow without assuming it is the only one.

The pack is organized into four phases that map to build order:
1. **Design foundation** — pack structure + visual/chat-UX design skills.
2. **Payment & commerce** — x402 payment states, agent purchase consent, spend controls.
3. **Implementation builder** — turns the above into running Next.js code.
4. **Quality & trust** — accessibility, trust copy, and component polish reviews.

## Tech Stack
- **Skills**: plain folders under `skills/<skill-name>/` each with a `SKILL.md` entry
  file using YAML frontmatter (`name`, `description`). The `description` drives invocation.
- **Spec management**: OpenSpec (`openspec/`) for spec-driven proposals and capabilities.
- **Target app stack** (what the skills generate, not this repo): **Next.js + Tailwind CSS
  + shadcn/ui**, with streaming responses, dark mode, and a mobile-responsive layout.

## Project Conventions

### Code Style
- Skill names are kebab-case and match their directory (`skills/frontend-design/`).
- One skill = one OpenSpec capability: single-purpose and self-contained.
- Implementation-oriented skills reference the shared stack convention rather than
  introducing a different framework or styling system.

### Architecture Patterns
- The `skill-pack` capability owns shared conventions (directory layout, `SKILL.md`
  format, stack); other skills reference it instead of redefining.
- Later skills compose earlier ones: the builder consumes the design and payment skills;
  reviewers run last over the builder's output.
- Payment UX states are grounded in real x402 mechanics (402 payment requirements →
  signed authorization → facilitator verify/settle → settlement receipt), and the exact
  header/field names follow the x402 spec and the chosen facilitator.

### Testing Strategy
- Specs assert the presence of concrete guidance (named states, checklists, anti-patterns),
  not subjective taste.
- Every change is validated with `openspec validate <change-id> --strict` before approval.

### Git Workflow
- `main` is the working branch for this greenfield pack.
- Follow the OpenSpec three-stage workflow: propose → (approve) → implement → archive.

## Domain Context
- **x402 / HTTP 402**: metered, account-less payments over HTTP.
- **Payment requirements**: the `402` response carries an `accepts` list of one or more
  payment requirements (scheme, network, asset, amount, recipient), so the client may have to
  choose among several accepted options (e.g. the same price as USDC on different networks).
- **Facilitator**: a service that verifies (`/verify`) and settles (`/settle`) payments so
  sellers need no blockchain infrastructure.
- **Stablecoin settlement**: gasless signed authorizations (EIP-3009, e.g. USDC/EURC) — the
  user *signs* an EIP-712 typed-data message, they do not manually broadcast an on-chain
  transaction.
- **Header/field-name drift**: exact header and field names are version-dependent and MUST
  NOT be hard-coded. The protocol's home moved from `coinbase/x402` to `x402-foundation/x402`,
  and header names changed across versions (earlier: `X-PAYMENT` / `X-PAYMENT-RESPONSE`;
  current foundation spec: `PAYMENT-REQUIRED` / `PAYMENT-SIGNATURE` / `PAYMENT-RESPONSE`).
  Treat these as illustrative; read names from the spec and chosen facilitator at build time.
- **Agentic commerce**: the chatbot may purchase paid APIs/tools autonomously within a
  configured budget, with explicit approval required above a threshold.

## Important Constraints
- Payment UI must be transparent and trustworthy: always answer "why am I paying, how much,
  and what do I get?" and keep spend visible and controllable.
- Avoid generic "AI" styling and a flashy "crypto dApp" look in favor of a serious,
  trust-forward aesthetic.

## External Dependencies
- The **x402 protocol specification** (source of truth for headers, payment requirements,
  scheme/network/asset fields): https://github.com/x402-foundation/x402 and https://www.x402.org/
- An **x402 facilitator** (e.g. Coinbase CDP) for payment verification and settlement.
