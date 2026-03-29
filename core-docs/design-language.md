# Design Language

Source of truth for visual design and interaction rules. Every UI change must comply with this document. If a pattern isn't documented here and it should be, add it.

---

## Core Principles

<!-- SETUP:
Ask the user: "What are 3-6 visual design principles for this project?
Examples: 'Content over chrome', 'Quiet confidence', 'Depth through layering not shadows',
'Typography does the hierarchy work'. If you don't have these yet, skip and fill in as
the design evolves."
-->

1. **[Populated by /init-project]**

## Typography

<!-- SETUP:
Ask the user: "What typeface(s) are you using? Do you have a type scale defined?
If you have a Figma file or existing tokens, point me there. Otherwise we can
define a minimal scale (title, heading, body, caption) and expand later."
-->

| Style | Size | Weight | Line Height | Use |
|-------|------|--------|-------------|-----|
| [Populated by /init-project] | | | | |

**Typeface:** [Populated by /init-project]

## Color System

<!-- SETUP:
Ask the user: "Do you have colors defined? (Figma tokens, CSS variables, SwiftUI Color extensions, etc.)
If yes, point me there. If not, what's the general direction?
(dark mode first? light and airy? monochrome with one accent? etc.)"
Define semantic tokens (textPrimary, backgroundSurface, accent) not raw hex values.
-->

| Token | Light | Dark | Use |
|-------|-------|------|-----|
| [Populated by /init-project] | | | |

## Spacing

<!-- SETUP:
Ask the user: "Do you have a spacing scale? Common options:
- 4px base (4, 8, 12, 16, 24, 32, 48)
- 8px base (8, 16, 24, 32, 40, 48)
- Custom
If unsure, 8px base is a solid default."
-->

| Token | Value | Use |
|-------|-------|-----|
| [Populated by /init-project] | | |

## Corner Radius

| Token | Value | Use |
|-------|-------|-----|
| `small` | [Populated by /init-project] | Buttons, inputs |
| `card` | | Cards, panels |
| `pill` | 999px | Tags, badges |

## Depth Model

<!-- SETUP:
Ask the user: "How do you handle layers and elevation?
Options: shadows, background color layering, blur/glass effects, or flat (no depth).
A common pattern is a 3-layer model: Navigation > Content > Float."
If too early to decide, leave a placeholder note.
-->

[Populated by /init-project]

## Component Guidelines

<!-- SETUP: Skip this section during init. It gets filled in as patterns emerge during development. Remove this comment but keep the empty subsections as scaffolding. -->

### Buttons
[Define as patterns emerge.]

### Cards
[Define as patterns emerge.]

### Empty States
[Define as patterns emerge.]

### Loading States
[Define as patterns emerge.]

## Animation

<!-- SETUP:
Ask the user: "Does this project use animation? If so, any direction on style?
(subtle and functional, playful, physics-based, minimal/none)"
If no animation, delete this section.
-->

- **Duration:** [Populated by /init-project]
- **Easing:** [Populated by /init-project]
- **Reduced motion:** [Fallback behavior]

## Review Checklist

Before considering any UI change complete:

- [ ] Uses design system tokens (no hardcoded values)
- [ ] Works in both light and dark mode (if applicable)
- [ ] Meets accessibility requirements
- [ ] Follows typography scale
- [ ] Follows spacing scale
- [ ] Animation respects reduced motion preference
