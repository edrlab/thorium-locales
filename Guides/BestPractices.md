# Best Practices

This document is a collection of best practices for translators and developers. 

Our reference is a subset of [i18next](https://www.i18next.com) that is meant to be used cross-platform (web, mobile, desktop).

## Allowed Features (Defined Subset)

We are using **interpolation and pluralization**. 

In particular, the following i18next features are excluded:

- unescaping (to mitigate XSS attacks)
- formatting
- nesting
- context
- objects and arrays

## General Rules

- Prefer strings in shared components over platform/product-specific strings
- Sentence and title case should be avoided when unnecessary as we can handle them with code and in context

## Naming Placeholder Variables

- It is expected that placeholder variables use pattern `p1`, `p2`, etc., which corresponds to the position of the placeholder in the string.
- The only exception to this rule is the `count` placeholder, which is used for plurals, as it is required by the i18n format.

Example:

```json
"xOfY": "{{ p1 }} of {{ p2 }}",
"positionsLeft": "{{ count }} positions left"
```

## Interpolation

Use interpolation for dynamic data (names, numbers, dates), but [do not use it to build sentences using translatable parts](https://www.i18next.com/principles/best-practices).

Example:

**DO:** `{{ count }} positions left`
**DON’T:** `Next {{ p1 }}` (`page`, `chapter`, `resource`, etc.)

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

For arabic, the following key names are used:

- `zero`
- `one`
- `two`
- `few`
- `many`
- `other`