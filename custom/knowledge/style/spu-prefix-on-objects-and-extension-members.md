---
bc-version: [all]
domain: style
keywords: [prefix, affix, spu, naming, object-name, tableextension, pageextension, as0011]
technologies: [al]
countries: [w1]
application-area: [all]
---

# StrongPoint objects and extension members carry the `SPU` prefix

## Description

In StrongPoint repositories every new AL object name, and every new field, control or action that a table extension or page extension adds to someone else's object, starts with the mandatory affix `SPU` — for example `codeunit 70760591 "SPU EMV Manager"` or the table-extension field `"SPU FB Receipt Printed"`. The AL-Go pipeline validates the prefix and fails the build without it; there is usually no `AppSourceCop.json` with `mandatoryAffixes` in the repository to warn earlier, so a missing prefix is only found at CI time.

## Best Practice

Name every new object `"SPU <App code> <Name>"` and every member added to a base-app or LS Central object `"SPU <App code> <Name>"`, following the app's existing code (for example `FB` for Fiscal Printing). Members of the extension's own `SPU` objects (fields of an `SPU` table, procedures of an `SPU` codeunit) do not need the prefix again. Report a missing prefix on a new object or extension member as `major`: the build will fail.

## Anti Pattern

A new object or an extension field without the prefix, a suffix instead of a prefix (`"Receipt Printed SPU"`), or another company's affix copied from sample code. Also wrong: demanding the prefix on members of an object that is already `SPU`-prefixed, or on existing objects that predate the rule.

## References

StrongPoint policy: AL-Go pipeline prefix validation in every SP repository (workspace `CLAUDE.md`, "AL Object Rules").
