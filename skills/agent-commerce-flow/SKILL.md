---
name: agent-commerce-flow
description: >-
  Use when designing the "the agent wants to buy or access something" experience — the
  consent and cost-preview UX shown when the chatbot calls a paid API, data source, or
  tool on the user's behalf. Triggers on "agent purchase", "agent buys/pays for", "paid
  tool/API call consent", "cost preview before charge", "spend approval", "autonomous
  vs. ask-first spending", or "budget threshold for the agent". Owns consent and the
  autonomous-vs-approval decision; the actual payment states live in x402-payment-ux and
  the budget/audit trail live in wallet-and-spend-control-ui. Uses frontend-design and
  chatbot-ui-designer conventions and the shared stack in ../README.md.
---

# Agent Commerce Flow — consent for agent-initiated spend

This skill owns the moment the **agent** (not the user directly) needs to spend money to
fulfill a request — calling a paid API, data source, or tool. The goal is consent the user
trusts: they always know *what* the agent wants to buy, *from whom*, *for how much*, and
*whether it needs their approval*.

The payment mechanics (402 → sign → settle → receipt) belong to `x402-payment-ux`; the
budget, limits, and audit trail belong to `wallet-and-spend-control-ui`. This skill is the
consent and decision layer between a user request and those.

## Consent surface — name the action, provider, and cost

When the chatbot needs to call a paid API or tool, present a **consent surface** before
proceeding that names:

- **The action** — what the agent intends to do ("fetch market data", "run this analysis").
- **The provider** — which paid API/tool/data source it will call.
- **The cost** — how much, before anything is charged.

This appears in-conversation (see `chatbot-ui-designer`'s agent-working / awaiting-user
states) so the purchase is part of the visible reasoning, not a hidden side effect.

## Itemized cost preview before any charge

Before any charge is made, show an **itemized preview** of what the agent intends to
purchase or access, including price. The user can review it before committing.

- Use the **actual price, asset, and network from the provider's `402` payment
  requirements** when available, rather than an estimated figure. Only fall back to an
  estimate when no `402` quote exists yet, and label it as an estimate.
- Itemize when multiple paid calls are bundled to fulfill one request (line items + total),
  so the user sees the whole cost, not just the first call.

## Autonomous within budget vs. explicit approval

Distinguish two paths by the configured budget (owned by `wallet-and-spend-control-ui`):

- **Within the autonomous budget** — the agent may **proceed autonomously**, without a
  blocking prompt. It still **records the action for the audit trail** owned by
  `wallet-and-spend-control-ui`, and the spend stays visible after the fact.
- **Over the autonomous threshold** — the agent **must get explicit user approval** before
  proceeding. The consent surface becomes a blocking confirmation (the awaiting-user state)
  and the agent does not spend until the user approves.

Keep the threshold and remaining budget legible at decision time so "why did this need my
approval?" is always answerable. Spend-limit handling (limit reached / exceeded) defers to
`wallet-and-spend-control-ui` and `x402-payment-ux`.

## Definition of done

- A consent surface names the action, provider, and cost before any paid call.
- An itemized cost preview (using real `402` requirements when available) is shown before a
  charge; bundled calls are itemized with a total.
- Within-budget actions proceed autonomously and are recorded to the audit trail;
  over-threshold actions require explicit approval before proceeding.
- The autonomous threshold and remaining budget are visible at the decision point.
