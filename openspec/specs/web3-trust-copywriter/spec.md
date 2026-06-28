# web3-trust-copywriter Specification

## Purpose
Writes clear, reassuring user-facing copy for the x402 chatbot's payment, wallet, consent,
error, and privacy surfaces, demystifying crypto-native metered payments in plain language
that does not scare or confuse non-crypto users.

## Requirements
### Requirement: Web3 Trust Copywriter Skill
The pack SHALL provide a `web3-trust-copywriter` skill that writes user-facing copy for
payment, wallet, consent, error, and privacy surfaces.

#### Scenario: Copy for a payment surface
- **WHEN** a payment, wallet, consent, error, or privacy surface needs user-facing text
- **THEN** the skill produces clear, reassuring copy appropriate to that surface

### Requirement: Demystify Crypto-Native Payments
The skill SHALL explain crypto-native, metered payments in plain language that does not
scare or confuse non-crypto users.

#### Scenario: Plain-language payment explanation
- **WHEN** copy explains why or how the user pays
- **THEN** the skill avoids unexplained jargon and frames the payment as transparent metered usage rather than a risky crypto action

