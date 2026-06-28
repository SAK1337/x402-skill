---
name: web3-trust-copywriter
description: >-
  Use when writing or reviewing user-facing copy for the x402 chatbot's payment, wallet,
  consent, error, and privacy surfaces. Triggers on "write the copy for", "payment/wallet
  microcopy", "consent text", "error message wording", "privacy notice", "explain the
  payment to users", or "make this less scary / less jargony". Produces clear, reassuring
  copy that demystifies crypto-native metered payments for non-crypto users. Pairs with
  the payment/commerce skills (whose states it labels) and uses the pack conventions in
  ../README.md.
---

# Web3 Trust Copywriter — copy that earns trust

This skill writes (or reviews) the **words** on every surface that touches money: payment,
wallet, consent, errors, and privacy. The goal is copy that is **clear and reassuring** —
the user always understands what's happening and never feels they're doing something risky.
The UI states themselves are owned by the payment/commerce skills; this skill labels them.

## Voice

- Plain, calm, and specific. Short sentences. Active voice.
- Honest about cost — always state the amount, asset, and what it buys. No hidden fees, no
  euphemisms.
- Reassuring without overpromising. Don't say "100% safe"; do say exactly what happens and
  what the user controls.

## Demystify crypto-native, metered payments

The single most important job: explain **why and how** the user pays in plain language that
does **not scare or confuse** a non-crypto user.

- **Avoid unexplained jargon.** If a term is unavoidable, define it inline in plain words.
  Prefer plain framings:
  - "gasless signed authorization" → "you approve the payment by signing — no transaction
    fees, no manual sending."
  - "EIP-3009 / settlement / facilitator" → "you're charged only the amount shown; it's
    confirmed automatically."
  - "402 Payment Required" → "this request costs a small amount to run."
- **Frame as transparent metered usage, not a risky crypto action.** It's "pay for what you
  use" — like metered API usage — not "send crypto into the unknown." Emphasize the amount is
  fixed and shown up front, and that approval is a signature, not handing over funds.

## Copy by surface

- **Payment** — what's being purchased, the exact price/asset/network, what unlocks, and a
  clear approve/decline. Answer "why am I paying, how much, what do I get?" in the copy.
- **Wallet** — connect/disconnect, balance, and what the connection lets the app do (and
  not do). Name the stablecoin and network plainly.
- **Consent (agent spend)** — what the agent wants to buy, from whom, for how much; whether
  it's within budget or needs approval. No surprise charges.
- **Errors** — say what happened, **whether the user was charged**, and the next step.
  Distinct, human wording for payment failed, insufficient balance (name asset + network +
  how to add funds), and spend-limit reached. Never blame the user; never leave them stuck.
- **Privacy** — plainly state what's stored, what's on-chain/public vs. private, and what
  the user controls.

## Output

When reviewing, flag jargon, vagueness, fear-inducing wording, and missing amounts — and
propose the replacement line. When writing, deliver final copy per surface, ready to drop in.
