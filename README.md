# 🌍 Shared locales between Thorium products

We're gradually moving to shared locales between Thorium products, which includes:

* [Thorium Desktop](https://github.com/edrlab/thorium-reader)
* [Thorium Web](https://github.com/edrlab/thorium-web)
* and Thorium Mobile

This repository is meant to host these locales, made available to our translators [through Weblate](https://hosted.weblate.org/projects/thorium-reader).

## Best Practices

A document listing best practices for translators and developers can be found [in guides](Guides/BestPractices.md).

## Formatting

All JSON locale files are formatted using [Prettier](https://prettier.io/) with alphabetically sorted keys. This ensures consistent formatting and reduces merge conflicts.

### Setup

```bash
npm install
```

### Commands

| Command | Description |
|---------|-------------|
| `npm run format` | Format all JSON files |
| `npm run format:check` | Check if files are properly formatted (used in CI) |

### Formatting Rules

- Keys are sorted alphabetically
- 4-space indentation

> [!NOTE]
> The CI will fail if JSON files are not properly formatted. Run `npm run format` before committing.
