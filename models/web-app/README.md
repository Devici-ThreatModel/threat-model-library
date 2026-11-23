# Web Application Reference Threat Model

A web application with supporting cloud services, with a focus on the web application.

**Scenario:** Web Application Architecture: Service-Based Application Layer Analysis

## In this folder

- [`web-app.otm.json`](web-app.otm.json): importable model (OTM 0.2.0). See [Importing into Devici](../../docs/importing-into-devici.md).
- [Components and data flow](components.md): every element, its role, and its attributes
- [Threats](threats.md): curated threats by theme, with likelihood, severity, priority, and recommended mitigations
- [`web-app-threats-and-mitigations.csv`](web-app-threats-and-mitigations.csv): download with full threat descriptions and mitigation guidance (implementation steps, rationale, examples, control category)
- [`web-app-components.csv`](web-app-components.csv): download of every component and data flow
- [Review notes](review-notes.md): what the model covers, and where it falls short

## At a glance

|  | Count |
|---|---|
| Curated threats documented here | 29 |
| Distinct mitigations | 56 |
| Threat-to-mitigation mappings | 83 |
| Threats in the full importable model | 134 |

The documentation covers the curated set we scored and prioritized. The importable model also includes every additional threat mapped to its components.

| Priority level | Threats |
|---|---|
| Critical | 6 |
| High | 15 |
| Medium | 7 |
| Low | 1 |

| Control type | Mitigations |
|---|---|
| Preventive | 48 |
| Detective | 7 |
| Corrective | 1 |

## System summary

The system is a cloud-hosted web application utilizing a service-oriented architecture. It serves external users via a web browser, employing a Content Delivery Network (CDN) for static assets and an API Gateway for routing requests. The backend consists of three distinct application services:
    - Content / Domain Data Service: Manages business data CRUD operations.
    - User Profile / Account Service: Handles user-specific profiles and billing data.
    - AuthC / AuthZ Service: Validates credentials and enforces access controls.
Service-to-service communication is restricted primarily to authorization validation. Data persistence follows a "database-per-service" pattern to ensure isolation. Supporting cloud components include an Identity Provider (IdP) for MFA/User management and a Centralized Logging Service.

## Assumptions

- The underlying cloud infrastructure provides a secure baseline (e.g., physical security, OS patching).
- The Identity Provider (IdP) securely handles cryptographic operations for MFA and token management.
- Internal service-to-service communication is contained within a private, restricted network.
