---
bc-version: [all]
domain: upgrade
keywords: [object-id, field-id, renumber, breaking-change, upgrade-codeunit, upgrade-tag, pipeline]
technologies: [al]
countries: [w1]
application-area: [all]
---

# Released object and field IDs never change in StrongPoint apps

## Description

Once any release of an SP app exists, the AL-Go pipeline rejects a change to an existing object ID or table field ID. Changing an ID is a schema break: installed tenants would lose the data in the old object or field. When data really has to move — a field replaced by a new one, a table split — the old element stays (marked obsolete), a new element gets a new ID, and an upgrade codeunit copies the data.

## Best Practice

Never renumber released objects or fields, even to tidy a range. For a data move, add the new object or field, mark the old one `ObsoleteState = Pending`, and migrate in a `Subtype = Upgrade` codeunit's `OnUpgradePerCompany`, one upgrade tag per step (`HasUpgradeTag` / `SetUpgradeTag`), with every tag registered in an `OnGetPerCompanyUpgradeTags` subscriber and matching install-code handling for new installs. `SPU FB Upgrade` in SP-LSC-Fiscal-Printing is the reference implementation. Report a changed released ID as `blocker`.

## Anti Pattern

Editing the number in `table 70760600` or `field(12; ...)` of a released object, deleting a released field instead of obsoleting it, or migrating data without an upgrade tag so it re-runs on every upgrade.

## References

StrongPoint policy: workspace `CLAUDE.md` ("Breaking change rule", "Upgrade Codeunits"); reference code `SP-LSC-Fiscal-Printing/.../SPUFBUpgrade.Codeunit.al`. Related shared rules: `microsoft/knowledge/upgrade/use-upgrade-tags-not-version-checks.md`, `microsoft/knowledge/upgrade/register-upgrade-tags-with-subscribers.md`, `microsoft/knowledge/breaking-changes/obsolete-table-fields-instead-of-deleting-them.md`.
