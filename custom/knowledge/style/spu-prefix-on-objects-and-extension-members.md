---
bc-version: [all]
domain: style
keywords: [prefix, affix, spu, sp, naming, object-name, tableextension, pageextension, as0011, pte, appsource]
technologies: [al]
countries: [w1]
application-area: [all]
---

# StrongPoint objects and extension members carry the app's prefix: `SPU` or `SP`

## Description

In StrongPoint repositories every new AL object name, and every new field, control or action that a table extension or page extension adds to someone else's object, starts with the app's prefix. Apps made from the AppSource template use `SPU`: their `.AL-Go/settings.json` sets `appSourceCopMandatoryAffixes` to `SPU`, and the AL-Go pipeline fails the build without it — for example `codeunit 70760591 "SPU EMV Manager"` or the table-extension field `"SPU FB Receipt Printed"`. Custom solutions and apps made from the PTE template use `SP`, for example `codeunit 60011 "SP Base Fiscal Receipt Mgt."`; nothing enforces it there, and a few newer custom apps use `SPU` instead.

## Best Practice

Take the prefix from `appSourceCopMandatoryAffixes` in `.AL-Go/settings.json` when it is set; otherwise follow the prefix the app's existing objects use, and use `SP` in a new custom or PTE app. Name new objects and members `"<prefix> <App code> <Name>"`, following the app's existing code (for example `FB` for Fiscal Printing). Members of the extension's own prefixed objects (fields of a prefixed table, procedures of a prefixed codeunit) do not need the prefix again. Report a missing prefix in an AppSource-template app as `major`, because the build will fail; in a custom or PTE app report it as `minor`. When the app's objects already use both prefixes, accept either.

## Anti Pattern

A new object or an extension field without the prefix, a suffix instead of a prefix (`"Receipt Printed SPU"`), or another company's affix copied from sample code. Also wrong: demanding `SPU` in a custom or PTE app whose objects use `SP`, or `SP` in an AppSource-template app; demanding the prefix on members of an object that is already prefixed, or on existing objects that predate the rule.

## References

StrongPoint policy: `appSourceCopMandatoryAffixes` in the AL-Go settings of AppSource-template repositories (validated by the pipeline); the `SP` convention in custom and PTE-template repositories such as SP-LEMORA-Base, sp-gelsva-base and SP-ANIS-Base.
