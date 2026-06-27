# x402 Skill Pack — Shared Conventions (`skill-pack`)

This file is the home of the **`skill-pack`** capability: the conventions every skill in
this pack shares. Individual skills reference this document instead of redefining the pack
structure, the `SKILL.md` format, or the target stack.

## Directory structure

Each skill lives in its own kebab-case subdirectory with a `SKILL.md` entry point:

```
skills/
  README.md                      # this file — shared conventions (skill-pack)
  frontend-design/SKILL.md
  chatbot-ui-designer/SKILL.md
  …                              # later phases add more
```

- A skill's directory name and its frontmatter `name` MUST match (`frontend-design/` ↔
  `name: frontend-design`).
- Adding a skill is purely additive: create `skills/<new-skill>/SKILL.md`. No existing
  skill directory needs to change.

## `SKILL.md` frontmatter format

Every `SKILL.md` begins with YAML frontmatter:

```yaml
---
name: <kebab-case, matches the directory>
description: <when to use this skill, including the phrases/situations that should invoke it>
---
```

- `name` — the invocation handle; matches the directory.
- `description` — drives invocation. State **when** the skill applies and the **trigger
  phrases** a user might say. This is what Claude matches against, so it must name concrete
  situations ("building the first version of the chatbot UI", "design the chat screen"),
  not just a topic.

The body after the frontmatter is the skill's guidance: instructions, checklists, named
states, and anti-patterns. Prefer concrete, checkable guidance over taste claims.

## Shared target stack

Everything this pack builds targets one stack. Implementation-oriented skills reference it
here rather than introducing a different framework or styling system:

- **Framework:** Next.js (App Router)
- **Styling:** Tailwind CSS
- **Components:** shadcn/ui
- **Baseline expectations:** streaming responses, dark mode, mobile-responsive layout.

Do not introduce a conflicting framework (e.g. plain CRA, Vue) or a competing styling
system (e.g. styled-components, Chakra) within a pack skill. If a skill needs to name the
stack, it points here.

## Composition order

Skills are built and composed in four phases by dependency direction:

1. **Design foundation** — `frontend-design`, `chatbot-ui-designer` (+ this `skill-pack`).
2. **Payment & commerce** — x402 payment UX, agent-commerce consent, spend controls.
3. **Implementation builder** — turns the above into running Next.js code.
4. **Quality & trust** — accessibility, trust copy, component polish reviews.

Later skills consume earlier ones; reviewers run last. See `openspec/project.md` for full
domain context and the x402 protocol notes.
