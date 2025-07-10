# 🌍 Shared locales between Thorium products

We're gradually moving to shared locales between Thorium products, which includes:

* [Thorium Desktop](https://github.com/edrlab/thorium-reader)
* [Thorium Web](https://github.com/edrlab/thorium-web)
* and Thorium Mobile

This repository is meant to host these locales, made available to our translators [through Weblate](https://hosted.weblate.org/projects/thorium-reader).

## Hints

* Prefer strings in shared components over platform/product-specific strings
* Plural forms should be handled using an object and the following key names: `zero`, `one` and `other`
* Use interpolated strings rather than substrings
* Sentence and title case should be avoided when unnecessary as we can handle them with code and in context
