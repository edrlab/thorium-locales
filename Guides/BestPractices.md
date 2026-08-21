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

### Compact vs Descriptive

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

### Labels vs. Counts

A plural key is always quantified: the code **must** always provide a `count` when requesting it. Code must never request a specific plural variant directly (e.g. `book_other`), since the set of variants and their grammatical case differ between languages.

When a word is displayed without a number (a section header, a menu item, a type label), it is not a plural but a plain label. Use separate non-plural keys:

- `x`: the singular label ("Author", "Book")
- `x_multiple`: the unquantified plural label ("Authors", "Books")
- `x_count_*`: the quantified plural forms ("{{ count }} authors")

Example:

```json
"author": "Author",
"author_multiple": "Authors",
"author_count_one": "{{ count }} author",
"author_count_other": "{{ count }} authors"
```

**DON'T:** display `author_other` as a label. In many languages, the `other` variant is a counting form (e.g. genitive or partitive case) that reads wrong without a number.

## Organizational Patterns

### Actions

Strings that trigger user actions (button labels, menu items, interactive controls) must always be structured as an object with `compact` and/or `descriptive` variants, even when only one variant is needed at the moment.

This ensures future-proofness: adding a missing variant later is a non-breaking change, whereas migrating a plain string to an object requires dropping all existing translations.

```json
"nextChapter": {
    "compact": "Next",
    "descriptive": "Next chapter"
}
```

If only one variant is currently needed, still use the object form:

```json
"addBookmark": {
    "compact": "Add bookmark"
}
```

### Empty States

Use an `emptyState` object to describe UI states where a list or section has no content to display. It is placed as a child of the feature key it belongs to.

An `emptyState` object always contains:

- **`title`**: Short heading shown to the user (e.g. "No bookmarks")
- **`description`**: Explanatory text. Can be a plain string or an object with named context variants when the reason for the empty state depends on the active filter or view mode.

### Simple empty state

Used when there is a single reason for the empty state:

```json
"bookmarks": {
    "emptyState": {
        "description": "No bookmarks added yet.",
        "title": "No bookmarks"
    }
}
```

### Empty state with context variants

Used when the empty state message changes depending on context (e.g. no filter applied vs. an active filter returning no results). Each variant is a named key under `description`:

```json
"bookshelf": {
    "emptyState": {
        "description": {
            "bookshelf": "Your bookshelf is empty. Start by adding your first book, audiobook, or comic to begin reading.",
            "filter": "No publications match this filter. Show your entire bookshelf to see all your titles.",
            "kind": "No publications match the selected type. Try showing all types to see more from your bookshelf."
        },
        "title": "No publications found"
    }
}
```
