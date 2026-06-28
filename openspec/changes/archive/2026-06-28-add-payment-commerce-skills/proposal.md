# Change: Add Payment & Commerce UX Skills

## Why
x402 is built on the HTTP `402 Payment Required` status code: a server answers a request with
`402` plus machine-readable payment requirements (price, network, asset, recipient), the
client returns a *signed stablecoin payment authorization* (gasless, e.g. EIP-3009 over USDC)
in the x402 payment header, and a facilitator verifies and settles it before the resource is
released. The chatbot therefore needs UI that makes these metered, account-less payments
understandable and trustworthy — clear states across the full request → 402 → sign → settle →
receipt round-trip, agent purchase consent, and visible spend controls. This change adds the
three skills that own that surface.

## What Changes
- Add the **x402-payment-ux** skill covering the full set of 402-driven payment states.
- Add the **agent-commerce-flow** skill for "the agent wants to buy/access something" UX.
- Add the **wallet-and-spend-control-ui** skill for wallet connection, budget caps, session
  and daily limits, and audit trail.

## Impact
- Affected specs: `x402-payment-ux` (new), `agent-commerce-flow` (new),
  `wallet-and-spend-control-ui` (new)
- Affected code: `skills/x402-payment-ux/`, `skills/agent-commerce-flow/`,
  `skills/wallet-and-spend-control-ui/`
- Depends on: `add-design-foundation-skills` (pack structure, SKILL.md format, shared stack)
