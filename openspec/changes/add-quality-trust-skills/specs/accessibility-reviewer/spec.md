## ADDED Requirements

### Requirement: Accessibility Reviewer Skill
The pack SHALL provide an `accessibility-reviewer` skill that checks the chatbot UI for
keyboard flow, color contrast, ARIA semantics, and loading states.

#### Scenario: Accessibility pass requested
- **WHEN** a user asks Claude to review the chatbot UI for accessibility
- **THEN** the skill checks keyboard navigation, color contrast, ARIA roles/labels, and loading states
- **AND** reports concrete issues with fixes

### Requirement: Focus Management for Payment Surfaces
The skill SHALL verify focus management for payment modals and dialogs, since these
interrupt the flow and must trap and restore focus correctly.

#### Scenario: Payment modal focus trapped
- **WHEN** a payment-required modal or dialog opens
- **THEN** the skill verifies focus moves into the dialog, is trapped within it, and returns to the trigger on close
