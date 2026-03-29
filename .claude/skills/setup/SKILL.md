---
name: setup
description: >
  Populate the project-specific template files (CLAUDE.md, spec.md,
  design-language.md) by interviewing the user or importing from existing
  material. Run this after copying the template into a new project.
disable-model-invocation: true
allowed-tools: Read, Edit, Write, Glob, Grep, Bash, WebFetch
effort: high
---

You are populating the project template files for this project. The template structure is already in place -- your job is to fill in the project-specific content.

## Step 1: Check for existing context

Ask the user:

> "Do you have any existing material I should work from -- a spec, brief, PRD, notes, Figma file, or anything else that describes this project? If so, point me to it (file path, URL, or paste it in)."

- If they provide a **file path**: read it and use it as the primary source. Ask clarifying questions only for gaps.
- If they provide a **URL**: fetch it and use as source material.
- If they **paste content**: use it directly.
- If they say **no / starting fresh**: proceed with the interview flow.

When working from existing material, restructure it into the template formats. Don't just copy it in. Ask the user to confirm anything ambiguous.

## Step 2: Populate project-specific files

Work through each file in order. Files have `<!-- SETUP: ... -->` comments with instructions on what to ask.

### 2a. CLAUDE.md

Read `CLAUDE.md`. For each `<!-- SETUP: ... -->` block:
- If you have source material that answers it, draft the content and confirm.
- If not, ask the questions specified in the SETUP comment.
- Replace the placeholder content (including the SETUP comment) with real content.

Keep the final CLAUDE.md under 80 lines. Ask 2-4 questions at a time, not all at once.

### 2b. spec.md

Read `core-docs/spec.md`. Same process.

### 2c. design-language.md

Ask: "Does this project have a visual UI component?"

- **No UI**: delete `core-docs/design-language.md` and remove the design language row from CLAUDE.md's doc table.
- **Existing design system**: ask where it lives and populate from that source.
- **New design system**: walk through the SETUP blocks.
- **Too early**: keep the scaffold, strip SETUP comments. Fill in later.

### 2d. Customize path patterns

Ask about project structure to update glob patterns in:
- `.claude/rules/ui.md` -- what paths contain UI/view files?
- `.claude/rules/safety.md` -- what files are safety-critical?

If the user doesn't know yet, leave the defaults.

### 2e. Web project features (conditional)

Based on the tech stack, determine if this is a web project (has a dev server) or native/CLI.

- If **web project**: keep `.claude/skills/link/SKILL.md` and `.claude/rules/dev-server.md`. Ask which port the dev server uses.
- If **not a web project**: delete `.claude/skills/link/` and `.claude/rules/dev-server.md`.

## Step 3: Clean up

Remove all remaining `<!-- SETUP: ... -->` comments from all files.

Tell the user: "Setup complete. You now have `/ship`, `/audit`, and agents (`claude --agent planner`, etc.). Want me to make the initial commit?"

## Interview principles

- Be concise. Don't explain the template -- just ask what you need to know.
- Group related questions (2-4 at a time).
- Short answers are fine. Write concise docs to match.
- Don't guess at product details -- ask.
- If the user has source material, lead with "Here's what I pulled from your notes -- anything to correct?" rather than re-asking.
