# Change: Add Quality & Trust Review Skills

## Why
AI-built UIs usually need a final pass for accessibility, trustworthy copy, and visual
polish — and a payment-handling crypto-native product needs this more than most. This change
adds three review skills that run last in the build order to raise the bar before shipping.

## What Changes
- Add the **accessibility-reviewer** skill (keyboard flow, contrast, ARIA, loading/focus states).
- Add the **web3-trust-copywriter** skill (user-facing copy for payment, wallet, consent,
  errors, and privacy).
- Add the **component-polish-reviewer** skill (spacing, hierarchy, hover states, responsive,
  microcopy).

## Impact
- Affected specs: `accessibility-reviewer` (new), `web3-trust-copywriter` (new),
  `component-polish-reviewer` (new)
- Affected code: `skills/accessibility-reviewer/`, `skills/web3-trust-copywriter/`,
  `skills/component-polish-reviewer/`
- Depends on: `add-design-foundation-skills` (pack structure); reviews the output of the
  builder and payment/commerce skills.
