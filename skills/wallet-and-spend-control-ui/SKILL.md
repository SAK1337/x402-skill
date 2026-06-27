---
name: wallet-and-spend-control-ui
description: >-
  Use when designing wallet and spend-control UI for the x402 chatbot — connecting a
  wallet, showing the stablecoin balance, setting budget/session/daily limits, and the
  audit trail of past spend. Triggers on "connect wallet", "wallet UI", "balance
  display", "budget cap", "spend limit", "session/daily limit", "remaining allowance",
  "transaction history", or "audit trail". Owns spend visibility and limits; the per-
  payment lifecycle lives in x402-payment-ux and agent-initiated consent lives in
  agent-commerce-flow. Uses frontend-design and chatbot-ui-designer conventions and the
  shared stack in ../README.md.
---

# Wallet & Spend Control UI — visibility and limits

This skill owns the **spend visibility** that agent commerce requires: connecting a wallet,
showing how much stablecoin is available, setting limits, and reviewing what was spent.
Because x402 settles via **gasless signed stablecoin authorizations**, center the balance on
the **payment asset** (e.g. USDC on the active network), not a generic native-token balance.

Per-payment states (402 → sign → settle → receipt) belong to `x402-payment-ux`; agent
purchase consent belongs to `agent-commerce-flow`. This skill is the wallet + controls
layer those rely on.

## Wallet connection and balance

- **Connection flow** — a clear connect/disconnect flow with connected-state feedback
  (which wallet, which network).
- **Balance display** — show the **relevant stablecoin balance for the active network** used
  for payments (e.g. USDC on Base), in the mono step from `frontend-design`. Make the asset
  and network unambiguous, since the same stablecoin exists on multiple networks. Avoid
  leading with a native-token balance — it's not what pays for x402 requests.

## Spend limits — budget, session, daily

Define configurable limits and always show **remaining allowance** against each:

- **Budget cap** — an overall ceiling on spend.
- **Session limit** — a cap per chat session.
- **Daily cap** — a cap per day.

Requirements:

- When a user sets any limit, **display the limit and the remaining allowance**.
- **Spending against a limit updates the remaining allowance** — keep it live so the user
  trusts the number.
- **Limit reached** — when spend reaches a configured limit, surface that clearly and link
  to **adjust it**. This coordinates with the **spend-limit-exceeded** state in
  `x402-payment-ux` (that skill blocks the individual payment; this skill explains the limit
  and offers adjustment).

These limits are the budget that `agent-commerce-flow` reads to decide autonomous-within-
budget vs. explicit-approval behavior.

## Audit trail

Provide a reviewable **audit trail** of payments and agent-initiated purchases:

- When the user opens it, show a **history of payments and agent purchases** with **amounts
  and timestamps** (and, where available, asset/network and the settlement reference from
  the receipt).
- It records both direct user payments and **autonomous agent purchases** made within budget
  (which `agent-commerce-flow` writes here), so nothing the agent spends is invisible.

## Definition of done

- A wallet connect flow and a stablecoin balance display (asset + network explicit, mono)
  exist.
- Budget cap, session limit, and daily cap are configurable, each showing remaining
  allowance that updates as spend occurs.
- A limit-reached state links to adjustment and coordinates with `x402-payment-ux`.
- An audit trail lists past payments and agent purchases with amounts and timestamps.
