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

> The skills themselves are being authored via OpenSpec change proposals (see below); the
> `skills/` directory is populated as each change is implemented.

## Spec-driven development (OpenSpec)

This project uses [OpenSpec](https://github.com/Fission-AI/OpenSpec) for spec-driven work.

```bash
openspec list                 # active change proposals
openspec show <change-id>     # view a proposal and its deltas
openspec validate --strict    # validate all changes/specs
```

- Proposals live in `openspec/changes/<change-id>/`.
- Conventions and domain context live in `openspec/project.md`.
- AI-assistant instructions live in `openspec/AGENTS.md`.

Current proposals:
- `add-design-foundation-skills`
- `add-payment-commerce-skills`
- `add-implementation-builder-skill`
- `add-quality-trust-skills`

## References
- x402 protocol: https://www.x402.org/ · https://github.com/x402-foundation/x402
- Coinbase x402 docs: https://docs.cdp.coinbase.com/x402/welcome
