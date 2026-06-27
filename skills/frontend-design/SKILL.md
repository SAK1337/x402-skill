---
name: frontend-design
description: >-
  Use when establishing the visual direction for the x402 chatbot front end or building
  its first UI version — mood, typography, color, spacing, and motion. Triggers on
  "build the chatbot UI", "first version of the interface", "design the look/feel",
  "make it look good/premium", "style the app", or any request to choose colors, fonts,
  or visual treatment for the chat or payment surfaces. Bias toward a distinctive,
  trust-forward, production-grade aesthetic; steer away from generic "AI" and flashy
  "crypto dApp" defaults. Pairs with chatbot-ui-designer (product/chat UX) and references
  the shared stack in ../README.md.
---

# Frontend Design — visual direction for the x402 chatbot

Your job under this skill is to give the x402 chatbot a **distinctive, production-grade,
trust-forward** visual identity — and to make sure that identity is decided *before*
any component is generated. The product moves real money over HTTP; the design has to
feel like something a person would trust with their wallet.

Target stack and baseline expectations (streaming, dark mode, responsive) live in
[`../README.md`](../README.md). Don't restate or override them here.

## Step 1 — Establish the visual direction FIRST

Before generating a single component, define and write down the direction. Do not skip
to building buttons and cards. Decide, in order:

1. **Mood / positioning.** One or two sentences: what should this feel like? Anchor it to
   "serious financial tool that happens to be a chatbot," not "fun AI toy." Name 1–2
   concrete reference points (e.g. a modern fintech dashboard, a well-made developer tool).
2. **Type scale.** Choose a typeface pairing and a modular scale (e.g. 1.25 ratio) with
   named steps (display / h1 / h2 / body / small / mono). Prefer a confident, legible
   sans for UI and a real monospace for amounts, addresses, and hashes — money and crypto
   identifiers should be unambiguous and tabular.
3. **Color system.** Define semantic tokens, not ad-hoc hex values: `background`,
   `surface`, `foreground`/`muted`, a single restrained `accent`, plus **financial
   status colors** (`success` for settled, `warning` for pending/awaiting-signature,
   `danger` for failed/declined). Ensure both light and dark themes. Keep the accent
   narrow — trust comes from restraint.
4. **Spacing rhythm.** Pick a base unit (4px or 8px) and a consistent scale. Generous,
   even spacing reads as premium; cramped or random spacing reads as templated.
5. **Motion principles.** Define when motion is allowed and how much: subtle, fast, and
   purposeful (state transitions, streaming, payment progress). Motion should clarify
   state, never decorate. No gratuitous animation around money.

Only after these are decided do you generate components — and every component must conform
to the tokens and scale you just defined.

## Step 2 — Generate components that conform to the direction

When you build components, derive them from the tokens above (Tailwind theme + shadcn/ui
variants). Amounts, balances, and addresses use the mono step; status uses the financial
status colors; spacing uses the base unit. Consistency *is* the premium feel.

## Trust-forward treatment for payment & wallet surfaces

Any surface that touches a payment, wallet, balance, signature, or spend limit gets the
**serious** treatment, not the flashy one:

- Calm, high-contrast, legible. The user must instantly read *what they're paying, how
  much, and what they get*.
- Status is communicated with the financial status colors and clear copy, not spectacle.
- No celebratory confetti, neon, glow, or token-mascot energy around transactions.
- Favor clarity and reversibility cues (confirm steps, visible amounts) over visual flair.

## Anti-patterns — do NOT do these

These are the templated defaults that make a product look generic or untrustworthy:

- **Purple/violet gradients** as the brand — the default "AI app" look. Avoid gradient
  hero backgrounds and gradient text as identity.
- **Generic "AI" tropes:** sparkle/✨ icons as primary branding, glassmorphism everywhere,
  a glowing orb, "powered by AI" chrome.
- **Flashy "crypto dApp" look:** neon-on-black, animated gradients, 3D coins, hype
  typography, aggressive glow/shadow. This actively *reduces* trust for a payments product.
- **Inconsistent ad-hoc styling:** raw hex values instead of tokens, mismatched spacing,
  more than one accent color, decorative motion on financial actions.
- **Default unstyled shadcn/ui** shipped as-is with no chosen direction — that's skipping
  Step 1.

## Definition of done

- A written visual direction (mood, type scale, color tokens incl. financial status,
  spacing unit, motion rules) exists before components.
- Components reference the tokens; amounts/addresses use mono; status uses status colors.
- Payment/wallet surfaces read as serious and trustworthy.
- None of the anti-patterns above are present.
