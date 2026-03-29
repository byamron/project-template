# Project Template

A reusable template for AI-assisted development with Claude Code. Designed to give Claude the best possible context for coding while capturing a rich history of design decisions and project context.

## Philosophy

This template enforces a documentation-first workflow where:
- Every meaningful change is documented with **why** and **tradeoffs**, not just what
- User feedback is synthesized into reusable rules
- Design decisions accumulate into a rich historical record for future context
- Claude gets consistent, scoped context through rules, agents, and skills

## What's Generalizable vs. Project-Specific

### Copy as-is (generalizable process)

These files enforce documentation discipline and agent workflow. They work across any project without modification:

| File | Purpose |
|------|---------|
| `.claude/agents/planner.md` | Scoping features, writing UX goals, updating plan.md |
| `.claude/agents/domain.md` | Data models, services, business logic |
| `.claude/agents/testing.md` | Writing and maintaining tests |
| `.claude/agents/docs.md` | Documentation updates and commits |
| `.claude/rules/general.md` | Documentation discipline, scope control, autonomy guardrails |
| `.claude/rules/safety.md` | Safety-critical code protection (customize `paths:`) |
| `.claude/rules/documentation.md` | Consistent formatting for history.md, feedback.md, plan.md |
| `.claude/skills/ship/SKILL.md` | Push/PR/merge workflow |
| `.claude/skills/audit/SKILL.md` | Pre-ship review against project standards |
| `.claude/settings.json` | Hooks enforcing doc updates and blocking secret writes |
| `core-docs/plan.md` | Living roadmap structure |
| `core-docs/history.md` | Decision log format |
| `core-docs/feedback.md` | Synthesized feedback format (FB-XXXX) |
| `core-docs/workflow.md` | Agent workflow and development process |

### Customize per project

These files contain project-specific content. Copy the structure, fill in your details:

| File | What to customize |
|------|-------------------|
| `CLAUDE.md` | Product brief, tech stack, principles, quality bar |
| `core-docs/spec.md` | Product vision, features, taxonomy |
| `core-docs/design-language.md` | Typography, colors, spacing, components |
| `.claude/agents/ui.md` | Paths in required reading, platform-specific rules |
| `.claude/rules/ui.md` | `paths:` patterns matching your project structure |
| `.claude/rules/safety.md` | `paths:` patterns matching your safety-critical files |

## Directory Structure

```
project/
├── CLAUDE.md                              # Entry point (~60-80 lines)
├── core-docs/                             # Living documentation
│   ├── plan.md                            # Roadmap + active work items
│   ├── history.md                         # Decision log (what, why, tradeoffs)
│   ├── feedback.md                        # Synthesized user feedback rules
│   ├── design-language.md                 # Visual/interaction source of truth
│   ├── spec.md                            # Product specification
│   └── workflow.md                        # Agent workflow + development process
├── .claude/
│   ├── settings.json                      # Hooks (doc enforcement, secret blocking)
│   ├── rules/                             # Auto-loading scoped rules
│   │   ├── general.md                     # Always loaded: doc discipline, scope control
│   │   ├── safety.md                      # paths: safety-critical files
│   │   ├── ui.md                          # paths: UI/view files
│   │   └── documentation.md              # Format rules for core-docs
│   ├── agents/                            # Claude Code agent specs
│   │   ├── planner.md                     # Scope + plan (no code)
│   │   ├── domain.md                      # Data + business logic
│   │   ├── ui.md                          # Views + interactions
│   │   ├── testing.md                     # Tests
│   │   └── docs.md                        # Documentation + commits
│   └── skills/                            # On-demand workflows
│       ├── setup/SKILL.md                 # Interactive template population
│       ├── ship/SKILL.md                  # Push, PR, merge
│       └── audit/SKILL.md                 # Pre-ship standards review
└── README.md                              # This file (delete for real projects)
```

## How the Pieces Work Together

### Context loading

| Layer | When loaded | Purpose |
|-------|-------------|---------|
| `CLAUDE.md` | Every session start | Persistent guidance (~80% adherence) |
| `.claude/rules/general.md` | Every session start (no `paths:`) | Process enforcement |
| `.claude/rules/safety.md` | When touching matching files | Safety reminders |
| `.claude/rules/ui.md` | When touching UI files | Design language enforcement |
| `.claude/settings.json` hooks | Deterministic events | 100% enforcement (doc updates, secret blocking) |
| Agent specs | When invoked | Role-specific context |
| Skills | When invoked | Workflow-specific context |
| `core-docs/*` | When agents read them | Living project knowledge |

### Enforcement levels

1. **Hooks** (100% enforced) -- doc update checks, secret file blocking
2. **Rules** (auto-loaded, advisory) -- design tokens, safety checks, doc formatting
3. **CLAUDE.md** (always loaded, advisory) -- project context, workflow summary
4. **core-docs/** (read on demand) -- detailed reference material

### Agent workflow

```
/clear → Planner Agent → update plan.md
/clear → Domain Agent  → models, services, logic
/clear → UI Agent      → views, interactions, styling
/clear → Testing Agent → tests
/clear → Docs Agent    → history.md, plan.md, commit → /ship
```

Use `/clear` between phases to keep context small. Each agent reads only the files it needs.

## Setup for a New Project

### Option A: Using `/init-project` (recommended)

If the personal skill is installed at `~/.claude/skills/init-project/`:

1. Create your project directory and `cd` into it
2. Run `git init`
3. Open Claude Code and run `/init-project`
4. It copies the template, interviews you to populate project-specific files, and offers to make the initial commit

### Option B: Manual copy + `/setup`

1. Copy this template into your project: `rsync -av --exclude='.git' --exclude='README.md' ~/Desktop/coding/project-template/ ./`
2. Open Claude Code in the project
3. Run `/setup` -- it walks through the same interview to populate project-specific files
4. Delete this README (or replace with your project's README)

### Option C: Fully manual

1. Copy the template files
2. Find all `<!-- SETUP: ... -->` comments in CLAUDE.md, spec.md, and design-language.md
3. Replace the placeholder content with your project details
4. Update `paths:` in `.claude/rules/ui.md` and `.claude/rules/safety.md` to match your project structure
5. Remove leftover SETUP comments

## Optional: Personal `/init-project` Skill

For faster project setup, you can create a personal skill that copies this template into any directory and runs the interactive setup in one step.

1. Clone this repo somewhere stable on your machine (e.g., `~/project-template`)
2. Create the skill directory: `mkdir -p ~/.claude/skills/init-project`
3. Create `~/.claude/skills/init-project/SKILL.md` with:

```yaml
---
name: init-project
description: >
  Initialize a new project with the documentation template. Copies the
  generalizable files from project-template, then interviews the user to
  populate project-specific docs.
disable-model-invocation: true
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
effort: high
---

Copy the template structure into the current working directory:

rsync -av --exclude='.git' --exclude='README.md' ~/path/to/project-template/ ./

Then run /setup to populate the project-specific files.
```

4. Update the `rsync` path to wherever you cloned this repo.

Now you can `cd` into any new project directory and run `/init-project` to get the full template + interactive setup.

---

## Key Concepts

### Documentation is part of "done"
The Stop hook in settings.json prompts Claude to update docs before finishing. history.md and plan.md must reflect reality at all times.

### Feedback is synthesized into rules
Raw user feedback is distilled into actionable rules (FB-XXXX format) so the same correction never needs to happen twice. These rules are the most valuable documentation for future context.

### History is a decision log, not a changelog
history.md captures **why** things were built the way they were -- options considered, tradeoffs discussed, lessons learned. This gives future sessions (and future you) the full context behind every decision.

### Rules auto-load by file path
Rules in `.claude/rules/` with `paths:` frontmatter only load when Claude touches matching files. This keeps context small while ensuring relevant rules are always present.

### Agents are roles, not sessions
Each agent spec defines a role with specific required reading, constraints, and output expectations. Use `/clear` between agents to keep context focused.
