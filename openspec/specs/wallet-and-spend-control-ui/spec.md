# wallet-and-spend-control-ui Specification

## Purpose
TBD - created by archiving change add-payment-commerce-skills. Update Purpose after archive.
## Requirements
### Requirement: Wallet and Spend Control UI Skill
The pack SHALL provide a `wallet-and-spend-control-ui` skill covering wallet connection,
stablecoin balance display, budget caps, session and daily limits, and an audit trail — the
spend visibility that agent commerce requires. Because x402 settles via gasless signed
stablecoin authorizations, the skill SHALL center the balance on the payment asset (e.g. USDC
on the active network) rather than a generic native-token balance.

#### Scenario: Wallet connection and balance
- **WHEN** a user connects a wallet to the chatbot
- **THEN** the skill defines the connection flow and a clear balance display for the relevant stablecoin and network used for payments

### Requirement: Spend Limits
The skill SHALL define configurable budget caps, per-session limits, and daily caps, and
SHALL show remaining allowance against each.

#### Scenario: Limits configured and visible
- **WHEN** a user sets a budget cap, session limit, or daily cap
- **THEN** the skill displays the limit and the remaining allowance
- **AND** spending against a limit updates the remaining allowance

#### Scenario: Limit reached
- **WHEN** spending reaches a configured limit
- **THEN** the skill surfaces that the limit is reached and links to adjust it (coordinating with the spend-limit-exceeded state in `x402-payment-ux`)

### Requirement: Audit Trail
The skill SHALL provide an audit trail of payments and agent purchases that the user can
review.

#### Scenario: Reviewing past spend
- **WHEN** a user opens the audit trail
- **THEN** the skill shows a reviewable history of payments and agent-initiated purchases with amounts and timestamps

