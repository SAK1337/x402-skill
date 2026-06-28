# frontend-design Specification

## Purpose
Establishes the distinctive, trust-forward visual direction — mood, type scale, color tokens,
spacing rhythm, and motion — for the x402 chatbot front end before any component is generated,
steering away from generic "AI" and flashy "crypto dApp" defaults.

## Requirements
### Requirement: Frontend Design Skill
The pack SHALL provide a `frontend-design` skill that guides Claude to produce distinctive,
production-grade web UI — strong typography, layout, color, and motion — for the x402
chatbot, and to avoid generic "AI-looking" defaults.

#### Scenario: Building the first UI version
- **WHEN** a user asks Claude to build the first version of the x402 chatbot interface
- **THEN** the `frontend-design` skill is invoked
- **AND** it directs Claude toward a premium, agent-commerce aesthetic rather than a generic chatbot look

#### Scenario: Avoiding generic styling
- **WHEN** the skill guides visual choices
- **THEN** it explicitly steers away from default purple-gradient "AI" styling and other templated defaults

### Requirement: Visual Direction Before Components
The skill SHALL instruct Claude to establish a visual direction — mood, type scale, color
system, spacing rhythm, and motion principles — before generating individual components.

#### Scenario: Direction established first
- **WHEN** Claude begins UI work under this skill
- **THEN** it defines the visual direction (typography, color, spacing, motion) first
- **AND** then generates components that conform to that direction

#### Scenario: Trust-forward aesthetic for payments
- **WHEN** the UI includes payment or wallet surfaces
- **THEN** the skill biases toward a serious, trustworthy visual treatment over a flashy "crypto dApp" look

