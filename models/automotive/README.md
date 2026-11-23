# Automotive Reference Threat Model

A connected vehicle: infotainment and user interface, ECUs, in-vehicle networks (CAN), ADAS, and wireless and telematics interfaces.

**Importable model:** [`automotive.otm.json`](automotive.otm.json)

## Scope

**In scope:** Infotainment, ECUs, vehicle networks, and external interfaces.

**Out of scope:** Manufacturing, dealer, and backend fleet infrastructure.

## Assumptions

An attacker may reach vehicle networks through wireless or physical ports.

## Known gaps

Backend fleet services and OTA update infrastructure are outside the model.

See [Importing into Devici](../../docs/importing-into-devici.md) to load this model.
