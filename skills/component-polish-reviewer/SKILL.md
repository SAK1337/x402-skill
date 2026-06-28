---
name: component-polish-reviewer
description: >-
  Use for a final refinement pass over the x402 chatbot UI — spacing, visual hierarchy,
  hover/interaction states, responsive behavior, and microcopy. Triggers on "polish the
  UI", "final pass", "tighten up the design", "review spacing/hierarchy", "check hover
  states", "responsive review", or "make it feel finished". A review skill: it proposes
  specific, targeted refinements that preserve functionality rather than redesigning from
  scratch. Runs last; references frontend-design for the tokens it checks against and the
  pack conventions in ../README.md.
---

# Component Polish Reviewer — the finishing pass

This is the **last** review skill: a refinement pass that takes a working UI from "fine" to
"finished." It is **targeted refinement, not a rebuild** — preserve all existing
functionality and structure; recommend small, specific changes. Check against the visual
direction established in `frontend-design` (tokens, scale, status colors).

## What to review

**Spacing**
- Consistent rhythm on the base unit (no ad-hoc margins); even, generous padding on cards
  and the payment surfaces; aligned edges and consistent gaps between repeated items
  (messages, line items, history rows).

**Visual hierarchy**
- The most important thing on each surface is the most prominent — on a payment card, the
  **amount and the primary action** lead; secondary info recedes. Type scale and weight used
  intentionally; one clear primary action per surface.

**Hover / interaction states**
- Every interactive element has hover, focus, active, and disabled states; transitions are
  subtle and fast (per `frontend-design` motion rules); loading/pending states (including
  verifying/settling) feel intentional, not janky.

**Responsive behavior**
- Layout holds from mobile to desktop: no overflow or truncation of amounts/addresses,
  touch-sized targets, composer and payment cards fully usable at small widths.

**Microcopy**
- Button labels, placeholders, tooltips, empty/error lines are crisp and specific. (Defer
  payment/wallet/consent wording to `web3-trust-copywriter`; here, catch generic labels like
  "Submit", awkward truncation, and inconsistent terminology.)

## How to recommend

- Propose **specific** refinements: location, the issue, and the exact change ("increase
  card padding from 12px to 16px to match the base unit"; "give the decline button a hover
  state").
- **Refinement over rebuild:** keep functionality and overall structure intact. If something
  needs a true redesign, flag it separately rather than quietly rewriting it.

## Output

A prioritized list of targeted refinements, each preserving existing functionality, ordered
by impact on the feel and clarity of the payment-handling surfaces first.
