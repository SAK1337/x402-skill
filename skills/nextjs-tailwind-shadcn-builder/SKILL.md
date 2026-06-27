---
name: nextjs-tailwind-shadcn-builder
description: >-
  Use when actually building/scaffolding the x402 chatbot front end in code — turning the
  design and payment specs into a running Next.js + Tailwind + shadcn/ui app. Triggers on
  "build the chatbot", "scaffold the app", "implement the UI", "set up Next.js/Tailwind/
  shadcn", "wire up streaming", "implement the 402 round-trip", "make it dark mode /
  responsive", or any request to write the front-end code. Composes the other pack skills
  (frontend-design, chatbot-ui-designer, x402-payment-ux, agent-commerce-flow,
  wallet-and-spend-control-ui) rather than redefining their behavior. Stack is fixed in
  ../README.md.
---

# Next.js + Tailwind + shadcn/ui Builder — implement the x402 chatbot

This is the **implementation** skill: it produces running code on the shared stack
([`../README.md`](../README.md)) by composing the earlier skills. It owns *wiring*
(scaffold, transport, the 402 retry loop, theming), not *behavior* — for visual direction,
chat states, and payment states it **references** the other skills instead of inventing new
variants.

## Compose, don't redefine

Pull behavior from the pack rather than re-specifying it:

- **`frontend-design`** — visual direction: theme tokens (Tailwind config), type scale,
  financial status colors, spacing, motion. Build the shadcn/ui theme from these.
- **`chatbot-ui-designer`** — chat layout and the response states (thinking / streaming /
  agent-working / awaiting-user), empty/error/mobile states, and the pre-coding checklist.
- **`x402-payment-ux`** — the full 402 payment lifecycle and failure states the round-trip
  drives.
- **`agent-commerce-flow`** — consent + itemized preview for agent-initiated spend.
- **`wallet-and-spend-control-ui`** — wallet connect, balance, limits, audit trail.

If you need a state or look that one of these owns, render *their* definition; do not create
a parallel one.

## Scaffold

Scaffold a project consistent with the shared stack convention:

- **Next.js** (App Router) + **TypeScript**.
- **Tailwind CSS** configured with the design tokens from `frontend-design`.
- **shadcn/ui** initialized; theme variables wired to those tokens (light + dark).
- Project structure: route handlers under `app/api/...` for server-side concerns (chat
  streaming proxy, facilitator integration), client components for chat + payment UI.

## Streaming assistant responses

Implement streaming so tokens render incrementally using the **streaming state from
`chatbot-ui-designer`**:

- Stream from a Next.js route handler (e.g. a streamed `Response` / web stream) and render
  tokens as they arrive; show the thinking state before the first token and allow stop.
- Drive the agent-working state when the assistant is taking actions (including paid ones),
  surfaced via `agent-commerce-flow`.

## The client 402 round-trip (core)

When a request the client makes returns **`402 Payment Required`**, implement this loop,
driving the UI defined by `x402-payment-ux` at each step:

1. **Parse payment requirements** from the `402` response — the `accepts` list (scheme,
   network, asset, amount, recipient). Build the quote from these, not from a client-side
   estimate. If more than one option is offered, drive the option-selection UI.
2. **Render the payment-required state** (`x402-payment-ux`): why paying, how much, what
   unlocks; user approves or declines.
3. **On approval, obtain a signed payment authorization** — the user *signs* a gasless
   stablecoin authorization (e.g. EIP-3009 over USDC, signed as EIP-712 typed data) with
   their connected wallet (`wallet-and-spend-control-ui`). This is a signature, not a
   broadcast transaction.
4. **Retry the request with the x402 payment header**, carrying the signed authorization.
5. **Handle verifying/settling** — settlement via the facilitator is asynchronous; render
   the distinct verifying/settling state until confirmed, then the **unlocked** state with
   the released content.
6. **On failure**, render the matching `x402-payment-ux` failure state (payment failed +
   retry, insufficient balance, spend-limit exceeded).

> **Header/field names are not hard-coded.** Read the exact payment-required / payment-
> signature / payment-response header and field names from the x402 spec and the chosen
> facilitator at build time (they have drifted across versions). Treat any literal names in
> examples as illustrative.

## Where settlement / facilitator integration is wired

Be explicit about the client/server split:

- **Client** — making the original request, detecting `402`, parsing requirements, driving
  the payment UI, and getting the user's **signature** (the wallet lives client-side).
- **Server (Next.js route handler)** — talking to the **facilitator** (verify/settle),
  holding any facilitator API keys/secrets, and constructing the payment header for the
  retried upstream call. Do not put facilitator credentials in client code.
- Keep the boundary clear: the client sends the signed authorization to your route handler;
  the route handler performs verify/settle (directly or via the facilitator) and returns the
  unlocked content plus settlement details.

## Settlement and receipt wiring

When the facilitator confirms settlement on the retried request:

- Surface the **unlocked content** in the chat stream.
- Record the **settlement details** (amount, asset, network, settlement/transaction
  reference) for the **receipt** surface (`x402-payment-ux`) and the **audit trail**
  (`wallet-and-spend-control-ui`) — including autonomous agent purchases.

## Dark mode and responsive layout

- **Dark mode** via the theme tokens (class-based theme toggle); both themes use the
  financial status colors from `frontend-design`.
- **Mobile-responsive** single-column layout per `chatbot-ui-designer`: composer above the
  keyboard, touch targets, payment/transaction cards legible at small widths.

## Definition of done

- A Next.js + Tailwind + shadcn/ui app scaffolded with the design tokens applied.
- Streaming responses render incrementally using the chatbot-ui-designer streaming state.
- The full client 402 round-trip works: parse requirements → payment UI → sign on approval
  → retry with payment header → verifying/settling → unlocked, with failure states handled.
- Facilitator integration is server-side (no client-side secrets); settlement details feed
  the receipt and audit trail.
- Dark mode and a mobile-responsive layout are present.
- Behavior is composed from the other pack skills, not redefined.
