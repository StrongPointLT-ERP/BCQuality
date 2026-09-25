---
bc-version: [all]
domain: web-services
keywords: [device, hardware, httpclient, sp-device-manager, payment-terminal, fiscal-printer, sco]
technologies: [al]
countries: [w1]
application-area: [all]
---

# Hardware devices are reached through SP Device Manager, not HttpClient

## Description

StrongPoint extensions talk to physical devices — payment terminals (EMV), fiscal printers, self-checkout terminals — only through the `SP Device Manager` app: its `SPU Device Manager` record (per store / POS terminal, holding device settings such as the fiscal protocol version) and the `SPU Device Manager` / `SPU Device Communication` codeunits, which exchange JSON with the Device Manager Windows service. Keeping device I/O in one place is what lets device settings, timeouts, logging and the service endpoint be managed per terminal.

## Best Practice

For new device interaction, read the device setup from the `SPU Device Manager` record and send requests through the Device Manager codeunits, following how the existing EMV and Fiscal Printing apps do it. Report a new direct `HttpClient` call to a device endpoint as `major`.

## Anti Pattern

A device integration that builds its own `HttpClient` request to a terminal or printer URL, stores device endpoints in its own setup table, or bypasses the per-terminal Device Manager record. Not a violation: `HttpClient` used for ordinary web services that are not devices (for example calls to external business APIs).

## References

StrongPoint architecture: `SP-Device-Manager` is the declared dependency for device I/O in SP-LSC-EMV-Integration, SP-LSC-Fiscal-Printing and SP-LSC-SCO-Integration (workspace `CLAUDE.md`, "SP-Device-Manager (Foundation)").
