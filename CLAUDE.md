# CLAUDE.md -- [Project Name]

## What This Is

<!-- SETUP:
Ask the user:
1. "What are you building? One sentence."
2. "Who is it for?"
3. "What's the core thesis -- the single idea that drives every decision?"
If working from an existing spec/brief, extract these directly and confirm.
Replace this entire section (including this comment) with 2-4 sentences and a core thesis line.
-->

[Populated by /init-project]

## Tech Stack

<!-- SETUP:
Ask the user:
1. "What platform? (iOS, web, Chrome extension, CLI, etc.)"
2. "What language and UI framework?"
3. "Any backend? What kind?"
4. "Any external APIs or AI models?"
5. "How is data stored?"
Keep only the lines that apply. Delete unused lines rather than leaving blanks.
-->

- **Platform:** [populated by /init-project]
- **Language/UI:** [populated by /init-project]
- **Backend:** [populated by /init-project]
- **Key APIs:** [populated by /init-project]
- **Persistence:** [populated by /init-project]

## Product Principles

<!-- SETUP:
Ask the user: "What are 3-6 principles that guide every decision in this project?
These aren't aspirational goals -- they're filters. If a feature doesn't serve
a principle, it doesn't ship. Examples:
  - Speed over features -- ship fewer things that work instantly
  - Minimal surface area -- if it doesn't serve the core use case, cut it
  - Privacy by default -- collect nothing beyond what's needed"
If the user struggles, ask: "What would you cut a feature over? What's non-negotiable?"
-->

- [Populated by /init-project]

## Core Documents

All project documentation lives in `core-docs/`. Review and update these as part of your workflow.

| Document | Path | Purpose |
|----------|------|---------|
| Plan | `core-docs/plan.md` | Living roadmap -- current focus, active work, completed features |
| History | `core-docs/history.md` | Decision log -- what was done, why, tradeoffs, branch+SHA |
| Feedback | `core-docs/feedback.md` | Synthesized user feedback distilled into rules |
| Design Language | `core-docs/design-language.md` | Visual/interaction source of truth (if applicable) |
| Spec | `core-docs/spec.md` | Product specification and feature definitions |

## Agent Workflow

Agents are defined in `.claude/agents/` and invoked via `claude --agent <name>` or by name in conversation.

| Agent | Role | When to use |
|-------|------|-------------|
| `planner` | Scope features, write UX goals, update plan.md | Starting or refining features |
| `domain` | Data models, services, business logic | Behavior or data structure changes |
| `ui` | Views, styling, interactions | Any UI/frontend work |
| `testing` | Unit tests, integration tests | After domain or UI changes |
| `docs` | History, doc updates, commits | Shipping completed work |

## How to Work

1. **Read before writing.** Check `core-docs/plan.md` for current focus and `core-docs/feedback.md` for past corrections.
2. **Follow the rules.** Scoped rules in `.claude/rules/` load automatically and enforce documentation discipline, scope control, and safety checks.
3. **Use agents.** See agent table above. Use `/clear` between agent phases.

## Quality Bar

<!-- SETUP:
Ask the user: "What does 'done' look like for this project? The defaults are:
Functional, Accessible, Performant, Clean, Crafted. Want to adjust any of these
or add specific targets (e.g., '<200ms response time', 'WCAG AA', '60fps scrolling')?"
Replace the bracketed items below with their answers. If defaults are fine, just remove the comment.
-->

Code doesn't ship unless it meets these standards simultaneously:

- **Functional:** Does what it's supposed to. Edge cases handled.
- **Accessible:** [Platform-appropriate accessibility standards met.]
- **Performant:** [Define your performance targets.]
- **Clean:** Follows project conventions. No dead code.
- **Crafted:** Feels intentional, not generated.
