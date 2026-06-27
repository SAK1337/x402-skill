## ADDED Requirements

### Requirement: x402 Payment UX Skill
The pack SHALL provide an `x402-payment-ux` skill that teaches Claude the UI states needed
to handle payments driven by the HTTP `402 Payment Required` status code.

#### Scenario: 402 response handled
- **WHEN** an API call returns HTTP `402 Payment Required`
- **THEN** the skill directs Claude to render a payment-required card that explains why payment is needed and shows the quote
- **AND** the user can approve or decline from that card

### Requirement: Full Payment State Coverage
The skill SHALL define UI for the complete payment lifecycle: free prompt, paid prompt
detected, `402 Payment Required`, payment quote displayed, user approves (signs) the payment,
payment submitted, payment verifying/settling (facilitator verify + on-chain settlement),
response unlocked, and a receipt / transaction history. The verifying/settling state SHALL be
distinct because settlement is asynchronous and may take time to confirm.

#### Scenario: Happy-path payment
- **WHEN** a paid prompt is detected and the user approves (signs) the displayed quote
- **THEN** the skill defines the submitted → verifying/settling → unlocked → receipt progression with visible state at each step

#### Scenario: Settlement in progress
- **WHEN** a signed payment has been submitted but the facilitator has not yet confirmed settlement
- **THEN** the skill shows a verifying/settling state so the user is not left wondering whether the payment is stuck

#### Scenario: Receipt available after payment
- **WHEN** a payment completes and the response is unlocked
- **THEN** the skill provides a receipt / transaction-history surface the user can review later
- **AND** the receipt reflects the settlement details returned by the facilitator (amount, asset, network, and a settlement/transaction reference)

#### Scenario: Multiple payment options offered
- **WHEN** a `402` response offers more than one accepted payment requirement (the `accepts` list contains several options, e.g. the same price as a stablecoin on different networks)
- **THEN** the skill defines how the user selects among the offered options before approving, rather than assuming a single fixed quote

### Requirement: Payment Failure States
The skill SHALL define distinct states for payment failed, insufficient balance, and spend
limit exceeded, each with a clear recovery or retry path.

#### Scenario: Insufficient balance
- **WHEN** a payment cannot proceed because the wallet's stablecoin balance (e.g. USDC on the required network) is too low to cover the quote
- **THEN** the skill shows an insufficient-balance state distinct from a generic failure, naming the required asset and network, with a path to add funds

#### Scenario: Spend limit exceeded
- **WHEN** a payment would exceed a configured spend limit
- **THEN** the skill shows a spend-limit-exceeded state explaining the limit and how to adjust it

#### Scenario: Payment failed with retry
- **WHEN** a submitted payment fails
- **THEN** the skill shows a failure state with a retry action

### Requirement: Payment Transparency
The skill SHALL require the UI to make clear, in plain language, why the user is being asked
to pay and what they receive in return.

#### Scenario: "Why am I paying?" answered inline
- **WHEN** a payment-required state is shown
- **THEN** the UI states what is being purchased, the price, and what unlocks on payment

### Requirement: States Grounded in x402 Protocol Mechanics
The skill SHALL map its UI states to the actual x402 protocol exchange so the generated UI
stays protocol-correct: the `402` response carries machine-readable payment requirements
(scheme, network, asset, amount, recipient); user approval produces a *signed payment
authorization* (not a separately broadcast transaction) sent back in the x402 payment header;
and verification/settlement is performed by a facilitator. The skill SHALL treat the exact
header and field names as defined by the x402 specification and the chosen facilitator rather
than hard-coding a single naming scheme.

#### Scenario: Quote derived from payment requirements
- **WHEN** a `402` response is received
- **THEN** the displayed quote (price, asset, network, recipient) is taken from the payment requirements in that response rather than invented client-side

#### Scenario: Approval is a signature, not a broadcast
- **WHEN** the user approves a payment
- **THEN** the skill frames the action as signing a stablecoin payment authorization that the facilitator settles, not as the user manually sending an on-chain transaction
