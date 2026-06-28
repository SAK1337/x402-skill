---
name: accessibility-reviewer
description: >-
  Use when reviewing the x402 chatbot UI for accessibility — keyboard navigation, color
  contrast, ARIA semantics, loading states, and focus management. Triggers on "a11y
  review", "accessibility review/audit", "is this keyboard accessible", "check contrast",
  "ARIA / screen reader", "focus management", or "is the payment modal accessible". A
  review skill: it reports concrete issues with fixes rather than redesigning. Runs last
  over the builder's output; uses the pack conventions in ../README.md.
---

# Accessibility Reviewer — a11y pass for the x402 chatbot

This is a **review** skill. Inspect the built UI and **report concrete issues, each with a
specific fix** (file/component + what to change). Do not silently rewrite the design — find
and recommend. A payment-handling product raises the stakes: a user who can't operate the
payment modal by keyboard or screen reader can't transact safely.

## What to check

**Keyboard navigation**
- Every interactive element (composer, send, approve/decline, wallet connect, option
  selection) is reachable and operable by keyboard alone, in a logical tab order.
- Visible focus indicators on all focusable elements (never `outline: none` with no
  replacement).
- No keyboard traps outside of intentional modal focus traps (see below).

**Color contrast**
- Text and meaningful UI meet WCAG AA (4.5:1 body, 3:1 large text / UI components) in both
  light and dark themes.
- The **financial status colors** (success/settled, warning/pending, danger/failed) are
  distinguishable and meet contrast — and status is never conveyed by color alone (pair with
  icon/text), since amounts and payment state must be unambiguous.

**ARIA semantics**
- Correct roles/labels: the chat log as a live region so streamed tokens are announced;
  buttons labeled by purpose ("Approve payment of 0.50 USDC", not "OK"); dialogs have
  `role="dialog"`/`aria-modal` and an accessible name.
- Don't over-ARIA: prefer native semantic elements; only add ARIA where native semantics
  fall short.

**Loading / async states**
- Thinking, streaming, and **verifying/settling** states are announced to assistive tech
  (live regions / `aria-busy`), so a non-sighted user knows a payment is in progress and not
  stuck.

## Focus management for payment surfaces (verify explicitly)

Payment modals/dialogs interrupt the flow and must manage focus correctly. For each payment
modal or dialog (payment-required, confirm, option selection):

- **Focus moves into the dialog** when it opens (to the dialog or its first actionable
  control).
- **Focus is trapped** within the dialog while open — Tab/Shift+Tab cycle inside it, and the
  background is inert.
- **Focus returns to the triggering element** when the dialog closes (approve, decline, or
  Escape).

## Output

Produce a findings list: each item names the location, the issue, its severity, and the
concrete fix. Prioritize anything that blocks completing or understanding a payment.
