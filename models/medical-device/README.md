# Medical Device Reference Threat Model

A connected therapy device, a patient's phone app, a gateway, and cloud stores for service data (patient-side) and medical data (clinician-side).

**Importable model:** [`medical-device.otm.json`](medical-device.otm.json)

## Scope

**In scope:** The device, phone app, gateway, and cloud data repositories.

**Out of scope:** Clinical workflows and regulatory submission content.

## Assumptions

The patient's phone is untrusted (BYOD); the device communicates directly with the phone.

## Known gaps

Identity provider, key management / HSM, BLE/network interface, and admin/support actors are not modeled; command replay, fail-safe failure on interrupted updates, and clinician insider abuse deserve explicit threats.

See [Importing into Devici](../../docs/importing-into-devici.md) to load this model.
