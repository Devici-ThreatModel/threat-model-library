# Medical Device Reference Threat Model

This model shows how medical data moves between devices, patient apps, cloud services, and clinicians across secure boundaries.

**Scenario:** Secure Telemetry & Feedback Loop for Connected Medical Devices

## In this folder

- [`medical-device.otm.json`](medical-device.otm.json): importable model (OTM 0.2.0). See [Importing into Devici](../../docs/importing-into-devici.md).
- [Components and data flow](components.md): every element, its role, and its attributes
- [Threats](threats.md): curated threats by theme, with likelihood, severity, and priority
- [Threat details](threat-details.md): how each attack works and which mitigations counter it
- [Mitigation library](mitigation-library.md): every mitigation with implementation guidance, rationale, and examples
- [Review notes](review-notes.md): what the model covers, and where it falls short

## At a glance

|  | Count |
|---|---|
| Curated threats documented here | 64 |
| Distinct mitigations | 116 |
| Threat-to-mitigation mappings | 179 |

| Priority level | Threats |
|---|---|
| Critical | 12 |
| High | 33 |
| Medium | 14 |
| Low | 2 |
| Unrated | 3 |

| Control type | Mitigations |
|---|---|
| Preventive | 101 |
| Detective | 11 |
| Corrective | 4 |

## System summary

This model shows how medical data moves between devices, patient apps, cloud services, and clinicians across secure boundaries.
The system is a connected health platform enabling the secure flow of medical data and device management.
- The Medical Device utilizes a Health Controller and OS to manage sensors and medical functions. It communicates locally with a patient's mobile device.
- The Patient’s Mobile App acts as the primary interface for visualization and a gateway for data transmission. It resides on the patient's phone alongside "other installed applications" and manages updates via an external App Store.
- The Backend Infrastructure is the central hub. An Infrastructure Gateway mediates all traffic, routing data to:
    - Patient-Facing Services: For user metrics and reports.
    - Clinician Services: For professional review and monitoring.
- Data Repositories: The cloud segregates data into Service Data (interactions) and Medical Data (clinical records).

## Scope

In Scope: Patient Devices (Sensors/Controller), Mobile Application, Backend Infrastructure (Gateway, Services, Storage), and Clinician interfaces.

## Assumptions

App Store Integrity: The model assumes the external App Store effectively ensures regulatory compliance and version integrity for the mobile app.

Mobile Connectivity: It is assumed the patient's phone is available and connected to forward sensor data to the infrastructure.

Gateway Efficacy: The Infrastructure Gateway is assumed to correctly mediate all communication and enforce access control without bypass.

OS Isolation: It is assumed the mobile OS provides sufficient isolation between the Medical App and "other installed applications."
