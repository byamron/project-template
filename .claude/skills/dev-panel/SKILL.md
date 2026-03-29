---
name: dev-panel
description: >
  Create a floating dev panel for live-tweaking UI properties (layouts, animations,
  styles, colors). Use when the user wants to experiment with values visually,
  tune animations, or dial in design tokens. Works for web (React, vanilla JS)
  and iOS (SwiftUI) projects.
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are building a floating dev/configurator panel for live-tweaking UI properties. The user wants to visually experiment with values using sliders and direct input.

## Step 1: Understand what to expose

Ask the user: "What properties do you want to tweak? For example: spacing, corner radius, colors, animation timing, shadow, opacity, blur, layout dimensions, etc."

Group their answers into 2-4 tabs/sections (e.g., "Layout", "Style", "Animation", "Color").

## Step 2: Detect platform and build

### For web projects (React/TypeScript)

Build a self-contained React component with these requirements:

**Panel container:**
- Fixed position, bottom-right by default (draggable is a bonus, not required)
- Collapsible to a small toggle button (icon or "Dev" label)
- Dark semi-transparent background (`rgba(26, 26, 26, 0.95)`), rounded corners, subtle shadow
- Width: 260-280px when expanded
- Max height: 400px with vertical scroll for content
- High z-index so it floats above everything
- Tab bar at top if multiple categories

**Each property gets a row with:**
- Label (left-aligned, small text)
- Slider input (`<input type="range">`) with visual fill bar
- Editable value display -- click to type a number directly, Enter to commit, Escape to cancel
- Slider and text input are connected: changing one updates the other
- Optional unit suffix (px, ms, %, deg, etc.)
- Value is clamped to min/max on commit

**Slider component pattern:**
```tsx
// Each slider needs: label, value, min, max, step, unit, onChange
// Display: smart formatting (integers show as whole, small decimals show 2-3 places)
// Input: range slider + clickable value that becomes a text input on click
```

**Connecting values to the UI -- use one of these patterns based on what's being tweaked:**

1. **CSS custom properties** (best for styles, spacing, colors):
   ```tsx
   document.documentElement.style.setProperty('--border-radius', `${value}px`)
   ```

2. **React state** (best for component props, layout logic):
   ```tsx
   const [config, setConfig] = useState({ borderRadius: 14, padding: 16 })
   // Pass config values as props or style values to target components
   ```

3. **Window state + listeners** (best for cross-component effects):
   ```tsx
   (window as any).__devConfig = config
   (window as any).__devListeners?.forEach(fn => fn())
   ```

**Footer:**
- "Copy Config" button that outputs the current values as a code snippet (CSS variables, JS object, or design tokens depending on what makes sense)
- "Reset" button to restore defaults

**Important implementation notes:**
- Import nothing external -- the panel is self-contained with inline styles
- Use `pointer-events: auto` on the panel, don't interfere with the page beneath
- The panel should be conditionally rendered (only in dev/debug builds if possible)
- Group the component in a single file for easy removal later

### For iOS projects (SwiftUI)

Build a SwiftUI overlay with these requirements:

**Panel container:**
- `.overlay` or `ZStack` approach, anchored to bottom-trailing
- Collapsible with a toggle button (SF Symbol `slider.horizontal.3`)
- Dark material background (`.ultraThinMaterial` or custom dark)
- Rounded corners, shadow
- ScrollView for content if it overflows

**Each property gets a row with:**
- Label (`.caption` or `.footnote` weight)
- `Slider(value:in:step:)` with min/max
- `TextField` bound to the same value via a NumberFormatter, or a custom binding that parses/formats
- Slider and text field are connected through the same `@State` or `@Binding`

**Connecting values:**
- Use `@State` properties in the panel, passed as `@Binding` to the target views
- Or use an `@Observable` config object shared via environment

**Footer:**
- "Copy" button that copies the current config as Swift code to clipboard (`UIPasteboard`)
- "Reset" button

**Important implementation notes:**
- Use `#if DEBUG` to compile-gate the panel
- Put it in a single file (e.g., `DevPanel.swift`)
- Attach to the root view as an overlay

## Step 3: Wire it up

After building the panel:
1. Identify where the tweakable properties are currently defined (hardcoded values, design tokens, state)
2. Replace those with references to the panel's config values
3. Set the panel's default values to match the current values in the code
4. Test that moving a slider updates the UI in real-time

## Step 4: Hand off

Tell the user:
- How to show/hide the panel
- That "Copy Config" gives them the final values to hardcode once they're happy
- That the panel file can be deleted (or compile-gated) before shipping

## Design principles for the panel

- **Compact** -- every pixel matters in a floating panel. Small text, tight spacing.
- **Non-blocking** -- never cover the content being tweaked. Bottom-right corner, collapsible.
- **Connected inputs** -- slider and text value are always in sync. This is non-negotiable.
- **Smart defaults** -- set min/max/step based on the property type (e.g., opacity: 0-1, step 0.01; border-radius: 0-40, step 1; duration: 0-1000ms, step 10).
- **Organized** -- group related properties into tabs. Don't dump 20 sliders in one list.
- **Removable** -- single file, no dependencies, easy to delete when done tweaking.
