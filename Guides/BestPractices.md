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
- arrays
- arbitrary objects

> [!IMPORTANT]
> Only [string variants](#string-variants) can use objects.

## General Rules

- Prefer strings in shared components over platform/product-specific strings
- Sentence and title case should be avoided when unnecessary as we can handle them with code and in context

## Naming Placeholder Variables

- Naming things is hard, so do not overcomplicate placeholder names; you can add descriptions and screenshots in Weblate to help translators understand the context.
- Placeholder names should be short and descriptive and stay consistent with their key.
- The only exception to this rule is the `count` placeholder, which is used for plurals and is required by the i18next format.
- A named placeholder should **never** be updated unless the string is being completely rewritten and all the translations must be dropped.

Example:

```json
"xOfY": "{{ x }} of {{ y }}",
"positionsLeft_one": "{{ count }} position left",
"positionsLeft_other": "{{ count }} positions left"
```

## Interpolation

Use interpolation for dynamic data (names, numbers, dates), but [do not use it to build sentences using translatable parts](https://www.i18next.com/principles/best-practices).

Example:

**DO:** `{{ count }} positions left`
**DON’T:** `Next {{ item }}` (where `item` is a translatable word like `page`, `chapter`, `resource`, etc.)

## String Variants

### compact vs descriptive

- **compact**: Short form for UI elements with space constraints (button labels, menu items, tabs)
- **descriptive**: Full form for accessibility labels (aria-label, screen readers, tooltips)

Example:

- Button text: "Next" (compact)
- Screen reader: "Next chapter" (descriptive)

## Plural Forms

Plural forms should be handled using the appropriate suffixes for the target language: 

- `zero` 
- `one`
- `two`
- `few`
- `many`
- `other`

> [!IMPORTANT]
> For plurals, the placeholder name **must** be `count`.

Example: 

```json
"positionsLeft_one": "{{ count }} position left",
"positionsLeft_other": "{{ count }} positions left"
```