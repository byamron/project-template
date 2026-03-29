# Workflow

How to work with Claude and agents on this project.

---

## Session Start Checklist

Before starting any work (~1 minute):

1. **Read `plan.md`** -- check "Current focus" and "Handoff Notes."
2. **Spot-check relevant docs** -- if relying on a design or architecture doc, verify key claims against the actual code.
3. **Pick your agent** -- see agent table in CLAUDE.md or use `claude --agent <name>`.

## Agent Workflow

For each piece of work, pick one primary agent. Full specs live in `.claude/agents/`.

### Standard feature workflow

```
1. Planner Agent   --> scope feature, write UX goals, update plan.md
2. Domain Agent    --> data models, services, business logic
3. UI Agent        --> views, styling, interactions
4. Testing Agent   --> tests for new behavior
5. Docs Agent      --> history.md, plan.md, commit
```

Use `/clear` between agent phases to keep context small.

### Quick recipes

**Bugfix:**
1. Testing Agent: write regression test reproducing the bug
2. Domain/UI Agent: fix until test passes
3. Docs Agent: update plan.md and commit

**Small UI tweak:**
1. UI Agent with plan.md + design-language.md + the view file
2. Docs Agent if the change is user-visible

**Feedback iteration (user corrects implementation):**
1. UI/Domain Agent: apply the corrected approach
2. Docs Agent: document feedback in feedback.md, update history.md

## Context Management

- **`/clear`** between agent phases and unrelated tasks
- **`/compact <focus>`** to keep relevant context while shedding noise
- **Specify files** -- each task should use 1 agent spec + plan.md + 1-5 code files
- **Skills load on-demand** -- use `/ship` or `/audit` instead of remembering workflows

## Documentation Is Part of "Done"

A feature is not complete until:
- `plan.md` is updated (mark completed items, update roadmap)
- `history.md` has a detailed entry (what, why, tradeoffs, decisions, branch+SHA)
- `feedback.md` captures any user corrections from the session

Update docs **before** committing, not after.

## 9-Step Development Process

1. **Clarify** -- ask questions about the request to ensure understanding
2. **Plan** -- design the approach before coding
3. **Execute** -- build the feature/fix
4. **Review** -- test and verify the implementation
5. **Present** -- show changes and explain key decisions
6. **Iterate** -- implement feedback
7. **Document** -- update plan.md, history.md, feedback.md
8. **Reflect** -- capture any problems or lessons learned
9. **Commit** -- push changes with descriptive message
