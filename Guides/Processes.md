# Processes

## Adding, removing, and updating strings

Adding and removing strings needs no special care: Weblate picks up new keys on its next scan, and removed keys simply disappear.

1. Lock the affected component in Weblate, so translators do not spend effort on keys that are about to disappear.
2. Merge any open Weblate pull request, and confirm the `weblate` branch is even with `main`.
3. Open the rename pull request. Apply the rename mechanically across all locale files.
4. Run `npm run format`, get the review, and merge.
5. Let Weblate re-scan, then unlock the component.

## Reviewing

It is required every change impacting locale strings is made through a pull request, and that it is reviewed by at least one maintainer of each projects involved.

## Merging

Before merging manual PRs, make sure to merge open Weblate PRs in order to avoid conflicts and issues. When applicable also merge Weblate PRs before every new release. 

If Copilot suggests modifications in a language you are not familiar with, add the fix as a suggestion on hosted Weblate. Otherwise proceed as you deem necessary.

## Contextualizing

It is expected that following a merge, translators will contextualize the new and updated strings in Weblate, if needed. They can explain what the string is used for, and provide examples of how it is used, as well as adding screenshots if relevant.