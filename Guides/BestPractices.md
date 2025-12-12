# Best Practices

This document is a collection of best practices for translators and developers.

## General Rules

- Prefer strings in shared components over platform/product-specific strings
- Use interpolated strings rather than substrings
- Sentence and title case should be avoided when unnecessary as we can handle them with code and in context

## Interpolation

Use interpolation for dynamic data (names, numbers, dates), but to not use it to build sentences using translatable parts.

Example:

**DO:** `{{ count }} positions left`
**DON’T:** `Next {{ x }}` (`page`, `chapter`, `resource`, etc.)

## String Variants

### compact vs descriptive

- **compact**: Short form for UI elements with space constraints (button labels, menu items, tabs)
- **descriptive**: Full form for accessibility labels (aria-label, screen readers, tooltips)

Example:

- Button text: "Next" (compact)
- Screen reader: "Next chapter" (descriptive)

## Plural Forms

Plural forms should be handled using an object and the following key names: 

- `zero` 
- `one`
- `other`

> [!IMPORTANT]
> For plurals, the placeholder name **must** be `count`.

Example: 

```json
"positionsLeft": {
  "one": "{{ count }} position left",
  "other": "{{ count }} positions left"
}
```