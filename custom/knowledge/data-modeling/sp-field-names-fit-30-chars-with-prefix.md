---
bc-version: [all]
domain: data-modeling
keywords: [field-name, length, al0468, 30-characters, prefix, tableextension]
technologies: [al]
countries: [w1]
application-area: [all]
---

# SP table field names, prefix included, stay within 30 characters

## Description

Table field names are limited to 30 characters (compiler rule AL0468), and StrongPoint's `sp.ruleset.json` raises AL0468 to an **error**. Because extension fields must start with `SPU ` plus the app code (for example `SPU FB `), only about 23–26 characters remain for the descriptive part. Generated names routinely exceed the limit and break the build.

## Best Practice

Count the full field name, prefix and spaces included, before proposing it; abbreviate the descriptive part (`Rcpt.`, `No.`, `Amt.`) the way existing SP fields do, and put the long wording in `Caption`. Report a field name over 30 characters as `major`.

## Anti Pattern

A field such as `"SPU FB Fiscal Receipt Printed Date Time"` (39 characters), or dropping the `SPU` prefix to make a name fit.

## References

StrongPoint policy: `sp.ruleset.json` — AL0468 `Error` ("Length of the table field name must not exceed 30 characters").
