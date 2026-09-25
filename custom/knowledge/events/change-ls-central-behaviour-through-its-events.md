---
bc-version: [all]
domain: events
keywords: [ls-central, lsc, event-subscriber, pos, integration, dependency, false-positive]
technologies: [al]
countries: [w1]
application-area: [all]
---

# Change LS Central behaviour through its events; calling its public codeunits is fine

## Description

StrongPoint extensions depend on LS Central. To change or extend what LS Central does — POS transaction flow, posting, printing, tender handling — SP code subscribes to LS Central events (`[EventSubscriber]` on `Codeunit::"LSC ..."`) instead of copying or re-implementing LS Central logic. Using LS Central's public codeunits as services is established SP practice and not a defect: `LSC POS Session`, `LSC POS Transaction`, `LSC POS Functions`, `LSC POS Print Utility`, `LSC WS Functions` and similar are called directly across all SP LSC apps.

## Best Practice

When the change alters LS Central's own behaviour, find the LS Central event that fires at that point and subscribe to it; state the event in the review if one exists. Call LS Central public procedures freely for session state, transaction data, printing and web-service helpers. LS Central source is not in Microsoft's Base App corpus — verify LS Central events against the project's `.alpackages` symbols.

## Anti Pattern

Duplicating an LS Central procedure body inside an SP codeunit to change one step of it, or modifying behaviour by re-running LS Central logic after the fact when an event exists. Equally wrong: flagging a direct call to a public LS Central codeunit as an architecture violation.

## References

StrongPoint practice observed in SP-LSC-Fiscal-Printing, SP-LSC-EMV-Integration, SP-LSC-SCO-Integration and SP-LSC-Discount-Management (event subscribers on LSC publishers alongside direct use of `LSC POS Session`, `LSC POS Transaction`, `LSC WS Functions`).
