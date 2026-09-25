---
bc-version: [all]
domain: style
keywords: [cyclomatic-complexity, lc0010, lintercop, maintainability, false-positive]
technologies: [al]
countries: [w1]
application-area: [all]
---

# Cyclomatic complexity (LC0010) is advisory in StrongPoint repositories

## Description

StrongPoint's `sp.ruleset.json` downgrades LinterCop LC0010 (cyclomatic complexity) to `Info`, and a few repositories disable it. Long procedures in POS, fiscal-printing and device flows mirror LS Central's own event and state handling; splitting them only to satisfy the metric is not required. Complexity is therefore never a merge gate in SP code.

## Best Practice

Mention high complexity at most as `info` or `minor`, and only together with a concrete readability or correctness problem you can point to (a duplicated branch, an unreachable path, a missing `else`). Judge new code on correctness first.

## Anti Pattern

Reporting a procedure as `major` or `blocker` because LC0010 fires or because it "has too many branches", or asking for a refactor of existing complex procedures that the change did not touch.

## References

StrongPoint policy: `sp.ruleset.json` — LC0010 `Info` ("Cyclomatic complexity warning changed to info").
