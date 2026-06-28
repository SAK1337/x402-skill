# x402 Skill Pack

A [Claude Code](https://claude.com/claude-code) **skill pack** for designing, building, and
reviewing polished, trustworthy chatbot front ends around
[**x402**](https://www.x402.org/) — internet-native payments over the HTTP `402 Payment
Required` status code.

> This repo is the *skill pack*, not the chatbot app. The skills guide Claude to generate
> the app on a shared stack (**Next.js + Tailwind CSS + shadcn/ui**).

## What is x402?

x402 lets services charge for APIs and content directly over HTTP, with no accounts or
API-key juggling:

1. The client requests a resource.
2. The server responds `402 Payment Required` with machine-readable payment requirements
   (price, network, asset, recipient).
3. The client returns a **signed, gasless stablecoin payment authorization** (e.g. EIP-3009
   over USDC) in the x402 payment header.
4. A **facilitator** verifies and settles the payment.
5. The server returns the resource plus settlement details.

This makes x402 a natural fit for **agentic commerce** — a chatbot paying for tools and data
on the user's behalf within a budget.

## The skills

Skills are organized in four build-order phases. Each lives under `skills/<name>/SKILL.md`
(YAML frontmatter `name` + `description`; the description drives invocation).

| Phase | Skill | Purpose |
|-------|-------|---------|
| 1. Design foundation | `frontend-design` | Distinctive, production-grade visual direction; avoid generic "AI" styling. |
| 1. Design foundation | `chatbot-ui-designer` | Chat layout, streaming/agent states, empty/error/mobile, pre-coding checklist. |
| 2. Payment & commerce | `x402-payment-ux` | Full 402 payment lifecycle, failure states, transparency — grounded in x402 mechanics. |
| 2. Payment & commerce | `agent-commerce-flow` | Agent purchase/access consent, itemized cost preview, autonomous-within-budget. |
| 2. Payment & commerce | `wallet-and-spend-control-ui` | Wallet connection, stablecoin balance, budget/session/daily caps, audit trail. |
| 3. Implementation | `nextjs-tailwind-shadcn-builder` | Turns the above into running code (streaming, 402 round-trip, dark mode, responsive). |
| 4. Quality & trust | `accessibility-reviewer` | Keyboard flow, contrast, ARIA, focus management for payment modals. |
| 4. Quality & trust | `web3-trust-copywriter` | Clear, reassuring copy for payment/wallet/consent/error/privacy surfaces. |
| 4. Quality & trust | `component-polish-reviewer` | Final pass on spacing, hierarchy, hover states, responsive, microcopy. |

> All nine skills are implemented and live under `skills/`. They were authored via OpenSpec
> change proposals (see below), which are now archived; their requirements are the canonical
> specs in `openspec/specs/`.

## Spec-driven development (OpenSpec)

This project uses [OpenSpec](https://github.com/Fission-AI/OpenSpec) for spec-driven work.

```bash
openspec list                 # active change proposals (none — all archived)
openspec list --specs         # canonical capability specs
openspec show <spec-id>       # view a capability spec
openspec validate --specs --strict   # validate all canonical specs
```

- Canonical capability specs live in `openspec/specs/<capability>/spec.md`.
- Archived proposals (their original deltas + tasks) live in `openspec/changes/archive/`.
- Conventions and domain context live in `openspec/project.md`.
- AI-assistant instructions live in `openspec/AGENTS.md`.

All four phase proposals have been implemented and archived, so there are no active changes:

| Proposal | Phase | Status |
|----------|-------|--------|
| `add-design-foundation-skills` | 1. Design foundation | ✅ implemented · archived |
| `add-payment-commerce-skills` | 2. Payment & commerce | ✅ implemented · archived |
| `add-implementation-builder-skill` | 3. Implementation | ✅ implemented · archived |
| `add-quality-trust-skills` | 4. Quality & trust | ✅ implemented · archived |

New work starts with a fresh proposal under `openspec/changes/` that modifies these
canonical specs (`propose → approve → implement → archive`).

## References
- x402 protocol: https://www.x402.org/ · https://github.com/x402-foundation/x402
- Coinbase x402 docs: https://docs.cdp.coinbase.com/x402/welcome
