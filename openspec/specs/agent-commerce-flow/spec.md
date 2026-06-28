# agent-commerce-flow Specification

## Purpose
Owns the consent and cost-preview UX for agent-initiated spend — naming the action, provider,
and itemized cost before any charge, and distinguishing actions the agent may take
autonomously within a configured budget from those that require explicit user approval.

## Requirements
### Requirement: Agent Commerce Flow Skill
The pack SHALL provide an `agent-commerce-flow` skill for the "the agent wants to buy or
access something" experience, used when the chatbot calls paid APIs, data sources, or tools.

#### Scenario: Agent requests a paid action
- **WHEN** the chatbot needs to call a paid API or tool to fulfill a request
- **THEN** the skill defines a consent surface that names the action, the provider, and the cost before proceeding

### Requirement: Itemized Cost Preview
The skill SHALL require an itemized preview of what the agent intends to purchase or access,
including price, before any charge is made.

#### Scenario: Cost preview before charge
- **WHEN** the agent is about to incur a charge on the user's behalf
- **THEN** the skill shows an itemized cost preview the user can review
- **AND** the preview uses the actual price, asset, and network from the provider's `402` payment requirements when available, rather than an estimated figure

### Requirement: Autonomous vs. Explicit Approval
The skill SHALL distinguish actions the agent may take autonomously within a configured
budget from actions that require explicit user approval.

#### Scenario: Within budget proceeds autonomously
- **WHEN** a paid action falls within the configured autonomous budget
- **THEN** the skill allows the agent to proceed and records the action for the audit trail owned by `wallet-and-spend-control-ui`

#### Scenario: Over threshold requires approval
- **WHEN** a paid action exceeds the autonomous threshold
- **THEN** the skill requires explicit user approval before the agent proceeds

