---
name: x402-payment-ux
description: >-
  Use when designing or building the UI for x402 payments — anything driven by an HTTP
  402 Payment Required response. Triggers on "402", "payment required", "payment flow",
  "pay for this API/response", "payment states", "payment quote", "settlement / receipt
  UI", "insufficient balance / payment failed states", or wiring the request → 402 →
  sign → settle → unlock round-trip into the chat. Owns the full payment lifecycle and
  failure states, grounded in real x402 mechanics. Pairs with agent-commerce-flow (who
  initiated the spend) and wallet-and-spend-control-ui (balance, limits, audit trail);
  uses the visual/chat conventions from frontend-design and chatbot-ui-designer and the
  shared stack in ../README.md.
---

# x402 Payment UX — the 402-driven payment lifecycle

This skill owns the UI for payments that flow through the HTTP **`402 Payment Required`**
status code. Render every state of the round-trip so the user always knows what is
happening with their money. Visual tokens come from `frontend-design`; payment surfaces
get its **trust-forward** treatment (financial status colors, mono for amounts/addresses).

## How x402 actually works (ground every state in this)

The UI must stay protocol-correct. The exchange is:

1. The client requests a resource.
2. If payment is needed, the server returns **`402`** with **machine-readable payment
   requirements** — an `accepts` list of one or more options, each carrying scheme,
   network, asset, amount, and recipient.
3. The client returns a **signed stablecoin payment authorization** (gasless, e.g.
   EIP-3009 `transferWithAuthorization` signed as an EIP-712 typed-data message over USDC)
   in the x402 payment header.
4. A **facilitator** verifies and settles it.
5. The server releases the resource plus settlement details.

Two consequences the UI must reflect:

- **The quote is derived, not invented.** Price, asset, network, and recipient shown to
  the user come from the payment requirements in the `402` response — never a client-side
  estimate.
- **Approval is a signature, not a broadcast.** When the user approves, they *sign* an
  authorization that the facilitator settles. Do not frame it as the user manually sending
  an on-chain transaction or paying gas.

> **Do not hard-code header/field names.** The spec and the chosen facilitator define exact
> names, and they have drifted across versions (e.g. earlier `X-PAYMENT` /
> `X-PAYMENT-RESPONSE`; current foundation spec `PAYMENT-REQUIRED` / `PAYMENT-SIGNATURE` /
> `PAYMENT-RESPONSE`). Read names from the spec/facilitator at build time; treat any names
> in examples as illustrative.

## The full payment state set

Define visible UI for each state. The user is never left guessing.

1. **Free prompt** — no payment needed; normal chat.
2. **Paid prompt detected** — the request will cost money; signal it *before* the user
   commits (e.g. a "this will require payment" affordance).
3. **402 Payment Required** — render a **payment-required card** that explains *why* payment
   is needed and shows the quote (see Transparency below). The user can **approve** or
   **decline** from this card.
4. **Quote displayed / option selection** — if the `402` `accepts` list offers more than
   one option (e.g. the same price as a stablecoin on different networks), let the user
   **select among the offered options** before approving — do not assume a single fixed
   quote. With one option, show it directly.
5. **Approve (sign)** — the user signs the payment authorization for the selected option.
6. **Submitted** — the signed authorization has been sent.
7. **Verifying / settling** — **a distinct state.** Settlement (facilitator verify +
   on-chain settlement) is asynchronous and may take time; show progress so the user is not
   left wondering whether the payment is stuck. Do not collapse this into "submitted."
8. **Unlocked** — settlement confirmed; the paid response is released and rendered.
9. **Receipt / transaction history** — a reviewable receipt the user can revisit later. It
   **reflects the settlement details returned by the facilitator**: amount, asset, network,
   and a settlement/transaction reference. The audit trail itself lives in
   `wallet-and-spend-control-ui`; this state is the per-payment receipt surface.

## Failure states (each distinct, each with a recovery path)

- **Payment failed** — a submitted payment failed; show what happened and a **retry**
  action.
- **Insufficient balance** — the wallet's stablecoin balance is too low for the quote.
  Distinct from a generic failure: **name the required asset and network** (e.g. "needs
  USDC on Base") and offer a path to **add funds**. (Balance display is owned by
  `wallet-and-spend-control-ui`.)
- **Spend limit exceeded** — the payment would exceed a configured spend limit. Explain the
  limit and link to **adjust it**, coordinating with the limit state in
  `wallet-and-spend-control-ui`.

## Payment transparency — answer "why am I paying?"

Whenever a payment-required state is shown, state in plain language:

- **What** is being purchased / what action it unlocks,
- **How much** — price, asset, and network (from the payment requirements),
- **What unlocks** on successful payment.

No hidden fees, no ambiguous "confirm" with no amount. The user should be able to answer
"why am I paying, how much, and what do I get?" without leaving the card.

## Definition of done

- Every lifecycle state (free → paid-detected → 402 → quote/selection → sign → submitted →
  verifying/settling → unlocked → receipt) has visible UI; verifying/settling is its own
  state.
- Multi-option `accepts` lists are selectable before approval.
- Payment-failed (retry), insufficient-balance (asset+network, add funds), and
  spend-limit-exceeded (adjust) are distinct states.
- The quote is derived from the `402` payment requirements; approval is framed as a
  signature; the receipt reflects facilitator settlement details.
- No header/field names are hard-coded as the only valid scheme.
