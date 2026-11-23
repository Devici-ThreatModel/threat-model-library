# Automotive Reference Threat Model

This model maps how a connected vehicle’s infotainment, ECUs, and networks exchange data for control, comfort, safety, and automation.

**Scenario:** Connected Vehicle Architecture: Infotainment, CAN Bus, and Cloud Integration

## In this folder

- [`automotive.otm.json`](automotive.otm.json): importable model (OTM 0.2.0). See [Importing into Devici](../../docs/importing-into-devici.md).
- [Components and data flow](components.md): every element, its role, and its attributes
- [Threats](threats.md): curated threats by theme, with likelihood, severity, and priority
- [Threat details](threat-details.md): how each attack works and which mitigations counter it
- [Mitigation library](mitigation-library.md): every mitigation with implementation guidance, rationale, and examples
- [Review notes](review-notes.md): what the model covers, and where it falls short

## At a glance

|  | Count |
|---|---|
| Curated threats documented here | 37 |
| Distinct mitigations | 74 |
| Threat-to-mitigation mappings | 85 |
| Threats in the full importable model | 38 |

The documentation covers the curated set we scored and prioritized. The importable model also includes every additional threat mapped to its components.

| Priority level | Threats |
|---|---|
| Critical | 8 |
| High | 20 |
| Medium | 7 |
| Low | 2 |

| Control type | Mitigations |
|---|---|
| Preventive | 67 |
| Detective | 4 |
| Corrective | 3 |

## System summary

The system represents the digital ecosystem of a modern connected vehicle, divided into interconnected domains:
- Infotainment System: The user-facing hub handling inputs (touch, voice, mobile devices via Bluetooth/USB) and multimedia, managed by an Infotainment OS.
- Onboard Computing System: The central processing unit that links infotainment features with vehicle controls and manages overall logic.
- CAN Bus Network: The critical internal network connecting various Electronic Control Units (ECUs), including Engine/Powertrain, Transmission, Braking/Safety, Body/Comfort, and Advanced Driver Assistance (ADAS).
- External Connectivity: Components like Wi-Fi and GPS extend the system to the cloud, enabling Over-the-Air (OTA) updates, telemetry, navigation, and internet media str

## Scope

In-Scope: The logical data and control flows between human interfaces (drivers/passengers), the onboard computing platform, the internal CAN bus network (ECUs), and external networks (Manufacturer Systems, Internet).

Out-of-Scope: Physical mechanical components (e.g., how the brakes physically apply friction), detailed internal circuit design of individual ECUs.

## Assumptions

- The Onboard Computing System effectively prioritizes traffic and filters malicious commands from reaching the CAN bus.
- External Wi-Fi networks and Manufacturer Systems are authenticated before allowing software updates.
