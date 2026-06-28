# nextjs-tailwind-shadcn-builder Specification

## Purpose
Implements the x402 chatbot front end on the shared stack by composing the design, chat, and
payment/commerce skills into running code — scaffolding, streaming responses, the client `402`
round-trip with server-side facilitator integration, settlement/receipt wiring, dark mode, and
a mobile-responsive layout.

## Requirements
### Requirement: Implementation Builder Skill
The pack SHALL provide a `nextjs-tailwind-shadcn-builder` skill that implements the x402
chatbot front end on the shared stack — Next.js, Tailwind CSS, and shadcn/ui — turning the
design and payment specs into running code.

#### Scenario: Scaffolding the app
- **WHEN** a user asks Claude to build the chatbot front end
- **THEN** the skill scaffolds a Next.js + Tailwind + shadcn/ui project consistent with the shared stack convention

### Requirement: Core Front-End Capabilities
The skill SHALL implement streaming assistant responses, client-side handling of the full
x402 `402` payment round-trip, dark mode, and a mobile-responsive layout.

#### Scenario: Streaming responses
- **WHEN** the assistant returns a streamed response
- **THEN** the implementation renders tokens incrementally with the streaming state from `chatbot-ui-designer`

#### Scenario: Client handles the 402 round-trip
- **WHEN** an API request from the client returns HTTP `402 Payment Required`
- **THEN** the implementation parses the payment requirements from the response, drives the payment-required UI defined by `x402-payment-ux`, and on approval obtains a signed payment authorization, retries the request with the x402 payment header, and handles the verifying/settling and unlocked states from the facilitator response

#### Scenario: Settlement and receipt wiring
- **WHEN** the facilitator confirms settlement on a retried request
- **THEN** the implementation surfaces the unlocked content and records the settlement details for the receipt/audit-trail surfaces

#### Scenario: Dark mode and responsive layout
- **WHEN** the app is built
- **THEN** it supports dark mode and a mobile-responsive layout

### Requirement: Composes Pack Skills
The skill SHALL consume the design, chatbot-ui, and payment/commerce skills as inputs rather
than re-specifying their behavior.

#### Scenario: Reuse over redefinition
- **WHEN** the builder needs visual direction, chat states, or payment states
- **THEN** it references `frontend-design`, `chatbot-ui-designer`, and the payment/commerce skills instead of defining new variants

