---
bc-version: [all]
domain: ui
keywords: [tooltip, page-field, aa0218, lc0064, inheritance, table-field-tooltip]
technologies: [al]
countries: [w1]
application-area: [all]
---

# StrongPoint page fields declare their own ToolTip

## Description

StrongPoint repositories configure CodeCop AA0218 as an **error** in `sp.ruleset.json` and disable LinterCop LC0064 (which suggests moving tooltips to the table field). The team observed tooltips defined only on the table field not showing in the client, so SP policy is a page-level `ToolTip` on every user-facing page field and action, regardless of runtime version. This overrides the general guidance to rely on table-field tooltip inheritance on runtime 13.0 and later.

## Best Practice

Declare `ToolTip` on each page field and action in SP pages and page extensions, even when the source table field also has one. Treat a user-facing page field without a page-level `ToolTip` as a `major` finding — AA0218 fails the SP build. Keep the text useful: say what the value is for, not "Specifies the <caption>".

## Anti Pattern

Recommending to remove page-level tooltips because the table field already has one, or to move them to the table (the LC0064 suggestion). Also wrong: accepting a page field with no page-level `ToolTip` on the grounds that it inherits one from the table.

## References

StrongPoint policy: `sp.ruleset.json` in SP repositories — AA0218 `Error` ("ToolTip property for page fields must be mandatory"), LC0064 `None` ("does not show in client if ToolTip missing in page"). Shared rule this overrides: `microsoft/knowledge/ui/bound-page-field-inherits-source-field-tooltip.md`.
