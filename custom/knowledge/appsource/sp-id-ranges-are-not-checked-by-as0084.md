---
bc-version: [all]
domain: appsource
keywords: [id-range, object-id, as0084, app-json, idranges, false-positive]
technologies: [al]
countries: [w1]
application-area: [all]
---

# StrongPoint ID ranges are governed by app.json, not by AS0084

## Description

StrongPoint's `sp.ruleset.json` disables AppSourceCop AS0084 ("We are using our custom range"). SP apps use StrongPoint-registered ranges such as `70760xxx` and, for some customer and test apps, other ranges; the rule that matters is that every object and extension field ID lies inside the app's own `app.json` `idRanges` and does not collide with another SP app.

## Best Practice

Check new IDs against the project's `app.json` `idRanges` (and the next free ID in that range). Report an ID outside `idRanges` as `major` — the compiler rejects it. Do not assess whether the range itself is an AppSource-assigned range.

## Anti Pattern

Reporting an SP app's ID range, or IDs inside it, as invalid because AS0084 or AppSource range rules would flag them; renumbering objects to move them into a different range (see the upgrade rule on ID changes after release).

## References

StrongPoint policy: `sp.ruleset.json` — AS0084 `None` ("Disable rule AS0084. We are using our custom range").
