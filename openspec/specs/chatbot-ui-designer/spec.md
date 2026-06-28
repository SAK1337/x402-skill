# chatbot-ui-designer Specification

## Purpose
Owns the chat product and interaction structure of the x402 chatbot — chat history, message
bubbles, the composer, and the assistant's streaming/thinking/agent-working states — plus
empty, error, and mobile states and a product-fundamentals checklist completed before coding.

## Requirements
### Requirement: Chatbot UI Designer Skill
The pack SHALL provide a `chatbot-ui-designer` skill that keeps the chat experience
coherent and polished, covering chat history, message bubbles, the message composer, and
agent/streaming response states.

#### Scenario: Designing the chat screen
- **WHEN** a user asks Claude to design or build the chat screen
- **THEN** the `chatbot-ui-designer` skill is invoked
- **AND** it specifies layout for chat history, message bubbles, and the composer

#### Scenario: Streaming and agent states
- **WHEN** the assistant is generating a response or acting as an agent
- **THEN** the skill defines streaming, thinking, and agent-working states with clear visual feedback

### Requirement: Empty, Error, and Mobile States
The skill SHALL require designing empty states, error states, and a responsive mobile
layout for the chat experience.

#### Scenario: First-run empty state
- **WHEN** a user opens the chatbot with no prior messages
- **THEN** the skill specifies a purposeful empty state that orients the user

#### Scenario: Error and mobile coverage
- **WHEN** the chat UI is designed
- **THEN** the skill covers error/failure states and a mobile-responsive layout

### Requirement: Product-Designer Pre-Coding Checklist
The skill SHALL require Claude to define product fundamentals before coding: target user,
chatbot personality, trust model, paid vs free interactions, primary conversion action,
empty state, error states, mobile layout, and transaction visibility.

#### Scenario: Checklist completed before implementation
- **WHEN** Claude is asked to build the chatbot UI under this skill
- **THEN** it first defines target user, personality, trust model, paid-vs-free interactions, and the primary conversion action
- **AND** only then proceeds to implementation

