---
paths:
  - "**/*View*"
  - "**/*Component*"
  - "**/*Screen*"
  - "**/*Page*"
  - "**/*Layout*"
  - "**/*.css"
  - "**/*.scss"
  - "**/*.tsx"
  - "**/*.vue"
  - "**/*.svelte"
  - "**/DesignSystem/**"
  - "**/design-system/**"
  - "**/components/**"
  - "**/views/**"
  - "**/screens/**"
  - "**/ui/**"
  - "**/styles/**"
---

# UI Implementation Rules

This file loads automatically when you touch UI-related files. Customize the paths above to match your project structure.

## Before making UI changes

1. Read `core-docs/design-language.md` -- it is the source of truth for visual decisions.
2. Read `core-docs/feedback.md` for any UI-related entries to avoid repeating known mistakes.

## Design system enforcement

- Use design system tokens for all visual values (colors, spacing, corner radius, typography, shadows, opacity).
- No hardcoded pixel values, color hex codes, or font sizes outside the design system.
- If a needed token doesn't exist, add it to the design system rather than hardcoding the value.

## Accessibility

- All interactive elements must be keyboard accessible and have appropriate accessibility labels.
- Respect reduced motion preferences for animations.
- Ensure color contrast meets WCAG AA standards (or platform equivalent).

## After making UI changes

- Run through the review checklist at the bottom of `core-docs/design-language.md`.
- If you discovered a UI pattern that failed or a working solution to a tricky problem, document it in `core-docs/feedback.md`.
