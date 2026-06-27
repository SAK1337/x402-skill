---
name: chatbot-ui-designer
description: >-
  Use when designing or building the chat experience of the x402 chatbot — the chat
  screen, message history, message bubbles, the composer/input, and the assistant's
  streaming / thinking / agent-working states. Triggers on "design the chat screen",
  "build the chat UI", "message bubbles", "chat layout", "streaming response UI",
  "agent state UI", "empty/error state for chat", or "make the chat mobile-friendly".
  Requires defining product fundamentals (the pre-coding checklist below) before any
  implementation. Pairs with frontend-design (visual direction) and references the shared
  stack in ../README.md.
---

# Chatbot UI Designer — the chat experience

This skill keeps the x402 chat experience **coherent, legible, and trustworthy** across
every state a real conversation goes through. Visual tokens (type, color, spacing, motion)
come from `frontend-design`; the stack comes from [`../README.md`](../README.md). This
skill owns *product and interaction structure*.

## Step 0 — Pre-coding checklist (define BEFORE implementing)

Do not write chat UI code until these product fundamentals are answered in writing. They
shape every later decision:

1. **Target user** — who is this for (consumer, developer, internal ops)? Sets tone and density.
2. **Chatbot personality** — voice and tone (e.g. concise expert vs. friendly guide).
3. **Trust model** — how the user knows the bot is acting safely with their money; what is
   shown, confirmed, and reversible.
4. **Paid vs. free interactions** — which messages/actions are free and which trigger an
   x402 payment, and how that distinction is signaled *before* the user commits.
5. **Primary conversion action** — the one thing the UI should make easy (e.g. approve a
   paid request, connect a wallet, complete a purchase).
6. **Empty state** — what a brand-new user sees and is guided to do first.
7. **Error states** — how failures (network, payment declined, signature rejected) appear.
8. **Mobile layout** — how the experience collapses to a single column / small screen.
9. **Transaction visibility** — how the user sees what they've paid and what's pending,
   without leaving the conversation.

Only after these are answered do you proceed to layout and components.

## Chat layout

- **Chat history** — vertical, newest at the bottom, auto-scroll on new content with a
  "jump to latest" affordance when the user has scrolled up. Group by turn; keep
  comfortable line length for readability.
- **Message bubbles** — clearly distinguish user vs. assistant (alignment + surface, not
  just color). Support rich content: text, code, and **payment/transaction cards** inline
  in the assistant stream. Long content wraps cleanly; addresses/amounts use the mono step.
- **Composer** — persistent input pinned to the bottom; multiline with send affordance,
  disabled/abled states, and room for an attachment or action affordance. On mobile it
  stays above the keyboard. Make the primary conversion action reachable from here.

## Response states — streaming, thinking, agent-working

The assistant is never just "loading." Define distinct, clearly-signaled states:

- **Thinking** — request accepted, no tokens yet: a quiet indicator, not a spinner-only.
- **Streaming** — tokens arriving: render incrementally with a caret/typing cue; keep the
  composer responsive (allow stop).
- **Agent working** — the bot is taking actions (calling a paid tool, fetching data,
  preparing a payment): show *what* it's doing as discrete steps, especially any step that
  costs money, so the user can follow and trust it.
- **Awaiting user** — when an action needs approval (e.g. confirm a payment), the stream
  pauses on a clear, blocking confirmation surface rather than proceeding silently.

Each state has visible feedback; motion is subtle and purposeful (see `frontend-design`).

## Empty, error, and mobile states

- **First-run empty state** — purposeful, not a blank screen. Orient the user: one line on
  what the bot does, what's free vs. paid, and 2–3 starter suggestions toward the primary
  conversion action.
- **Error / failure states** — handle at least: network/timeout, payment declined,
  signature rejected/expired, and insufficient balance. Each shows what happened, whether
  the user was charged, and a clear recovery action. Never fail silently.
- **Mobile-responsive layout** — single column, composer above the keyboard, touch-sized
  targets, history that scrolls under a compact header. Payment/transaction cards remain
  fully legible at small widths.

## Definition of done

- The Step 0 checklist is answered before implementation.
- Layout covers history, bubbles, and composer with rich/payment content support.
- Thinking, streaming, agent-working, and awaiting-user states are all defined with
  visible feedback.
- A purposeful empty state, the enumerated error states, and a mobile layout are specified.
- Transaction visibility is present without leaving the conversation.
