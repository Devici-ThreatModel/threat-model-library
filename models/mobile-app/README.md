# Mobile App Reference Threat Model

This model shows how a mobile app handles user input, authentication, storage, and communication within sandboxed and cloud systems.

**Scenario:** Mobile Application Architecture: Data Flow & Sandbox Integration

## In this folder

- [`mobile-app.otm.json`](mobile-app.otm.json): importable model (OTM 0.2.0). See [Importing into Devici](../../docs/importing-into-devici.md).
- [Components and data flow](components.md): every element, its role, and its attributes
- [Threats](threats.md): curated threats by theme, with likelihood, severity, priority, and recommended mitigations
- [`mobile-app-threats-and-mitigations.csv`](mobile-app-threats-and-mitigations.csv): download with full threat descriptions and mitigation guidance (implementation steps, rationale, examples, control category)
- [`mobile-app-components.csv`](mobile-app-components.csv): download of every component and data flow
- [Review notes](review-notes.md): what the model covers, and where it falls short

## At a glance

|  | Count |
|---|---|
| Curated threats documented here | 42 |
| Distinct mitigations | 59 |
| Threat-to-mitigation mappings | 88 |
| Threats in the full importable model | 58 |

The documentation covers the curated set we scored and prioritized. The importable model also includes every additional threat mapped to its components.

| Priority level | Threats |
|---|---|
| Critical | 8 |
| High | 20 |
| Medium | 10 |
| Low | 4 |

| Control type | Mitigations |
|---|---|
| Preventive | 54 |
| Detective | 4 |
| Corrective | 1 |

## System summary

The system represents a mobile application operating within a secure mobile operating system environment. The core structure is defined by the Mobile App Sandbox, which isolates the application execution. Key components include:
- User Interface (UI): Captures user input and displays data.
- Application Logic: The central controller managing communication between internal components (Local Auth, Credential Storage, App Store Client) and external endpoints.
- Storage Layer: Consists of Application Storage (private cache), Credential Storage (secure tokens), and Shared Storage (data exchange).
- External Integration: The app communicates via encrypted network channels with Application Services (Backend APIs), OAuth 2.0 / OpenID Connect Providers (Identity), and the App Store.

## Scope

In-Scope: The logical flow of data within the mobile device, the interaction between the User and the UI, the internal mechanics of the App Sandbox (logic, storage), and the interfaces to external systems.

Out-of-Scope: The internal implementation details of the cloud services and the App Store backend; these are treated as external entities.

## Assumptions

The Mobile Operating System correctly enforces sandbox isolation and app permissions.

Network communication is protected by standard encryption (TLS) and is not intercepted (e.g., no hostile proxies).

Authentication follows standard OAuth 2.0 / OpenID Connect flows without customization deviations.
