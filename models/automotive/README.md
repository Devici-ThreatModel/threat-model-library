# Automotive Reference Threat Model

This model maps how a connected vehicle’s infotainment, ECUs, and networks exchange data for control, comfort, safety, and automation.

**Scenario:** Connected Vehicle Architecture: Infotainment, CAN Bus, and Cloud Integration

## In this folder

- [`automotive.otm.json`](automotive.otm.json): importable model (OTM 0.2.0). See [Importing into Devici](../../docs/importing-into-devici.md).
- [Components and data flow](components.md): every element, its role, and its attributes
- [Threats](threats.md): curated threats by theme, with likelihood, severity, priority, and recommended mitigations
- [`automotive-reference.xlsx`](automotive-reference.xlsx): Excel workbook download with the full model on separate tabs (overview, components, threats, mitigations with guidance, review notes)
- [Attack paths](attack-paths.md): six entry-point-to-impact paths read across the threats
- [Standards mapping](standards-mapping.md): indicative mapping to ISO/SAE 21434 impact categories, UN R155 and UN R156
- [Review notes](review-notes.md): what the model covers, where it falls short, and how it scores against the scorecard

## At a glance

|  | Count |
|---|---|
| Curated threats documented here | 39 |
| Distinct mitigations | 90 |
| Threat-to-mitigation mappings | 98 |
| Threats in the full importable model | 40 |

The documentation covers the curated set we scored and prioritized. The importable model also includes every additional threat mapped to its components.

| Priority level | Threats |
|---|---|
| Critical | 8 |
| High | 22 |
| Medium | 7 |
| Low | 2 |

| Control type | Mitigations |
|---|---|
| Preventive | 74 |
| Detective | 9 |
| Corrective | 7 |

## Version 2

Version 2 draws the four hardware components that version 1's review notes identified as missing: the **Central Gateway ECU**, the **OBD-II port** (with a diagnostic tool or aftermarket dongle), the **hardware security module**, and the **keyless entry receiver** (with its key fob). The five ECU data flows that ran straight to the onboard computer now run through the gateway.

It also adds two threats (keyless entry relay and replay attacks, and HSM compromise or misuse of key operations), and moves gateway, diagnostic, OTA, and key-handling threats onto the components they actually affect. Generic, mismatched, and duplicate mitigations were replaced with ones that name a component and a mechanism, and every Critical threat now has at least one detective or corrective control. Version 1 remains in the git history.

## How priority is set

Priority is the author's expert judgment of context, not a formula. Likelihood and severity inform it but do not determine it: the same pair can earn different priorities for different threats, for example High likelihood with High severity is High for diagnostic interface exploitation and Critical for broken authentication. Re-prioritize with your own likelihood and severity when you adapt the model.

## System summary

The system represents the digital ecosystem of a modern connected vehicle, divided into interconnected domains:
- Infotainment System: The user-facing hub handling inputs (touch, voice, mobile devices via Bluetooth/USB) and multimedia, managed by an Infotainment OS.
- Onboard Computing System: The central processing unit that links infotainment features with vehicle controls and manages overall logic.
- Central Gateway: A dedicated gateway ECU between the onboard computer and the CAN bus that separates network domains, filters cross-domain traffic, and enforces diagnostic access policy.
- CAN Bus Network: The critical internal network connecting various Electronic Control Units (ECUs), including Engine/Powertrain, Transmission, Braking/Safety, Body/Comfort, and Advanced Driver Assistance (ADAS).
- Physical Access: The OBD-II diagnostic port, used by diagnostic tools and aftermarket dongles, and the keyless entry receiver that listens for the key fob and feeds the Body/Comfort ECU.
- Hardware Security Module: A crypto chip in the computing system that holds keys and verifies signatures for secure boot, OTA updates, and message authentication.
- External Connectivity: Components like Wi-Fi and GPS extend the system to the cloud, enabling Over-the-Air (OTA) updates, telemetry, navigation, and internet media streaming.

## Scope

In-Scope: The logical data and control flows between human interfaces (drivers/passengers), the onboard computing platform, the internal CAN bus network (ECUs), and external networks (Manufacturer Systems, Internet).

Out-of-Scope: Physical mechanical components (e.g., how the brakes physically apply friction), detailed internal circuit design of individual ECUs.

## Assumptions

- The Central Gateway ECU enforces segmentation between network domains and filters malicious commands before they reach the CAN bus, and the Onboard Computing System prioritizes traffic behind it.
- External Wi-Fi networks and Manufacturer Systems are authenticated before allowing software updates.

## Known gaps

- No cellular telematics unit, V2X communication, or EV charging interface is drawn.
- Security modules embedded in individual ECUs are not drawn; the HSM is modeled once, in the computing system.
- No TARA risk values or ASIL ratings are calculated. See the [standards mapping](standards-mapping.md).
- Some mitigations imported from the Devici library remain generic. See the [review notes](review-notes.md).
