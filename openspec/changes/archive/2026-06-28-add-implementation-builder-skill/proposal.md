# Change: Add Implementation Builder Skill

## Why
The design and payment/commerce skills define *what* the x402 chatbot should look like and
*how* payments behave. We still need a skill that turns those specs into running code on the
chosen stack. This change adds the implementation skill that scaffolds and builds the front
end in Next.js + Tailwind + shadcn/ui, consuming the earlier skills.

## What Changes
- Add the **nextjs-tailwind-shadcn-builder** skill that implements the chatbot front end on
  the shared stack.
- The skill composes the design, chatbot-ui, and payment/commerce skills rather than
  re-specifying their behavior.

## Impact
- Affected specs: `nextjs-tailwind-shadcn-builder` (new)
- Affected code: `skills/nextjs-tailwind-shadcn-builder/`
- Depends on: `add-design-foundation-skills` and `add-payment-commerce-skills` (this skill
  consumes their outputs and the shared stack convention)
