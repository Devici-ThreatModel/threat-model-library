# LLM and Agentic Systems Reference Threat Model

This model shows how an LLM system handles data flow between users, agents, models, and external sources across trust boundaries.

**Scenario:** LLM System Architecture: RAG, Agents, and External Integrations

## In this folder

- [`llm.otm.json`](llm.otm.json): importable model (OTM 0.2.0). See [Importing into Devici](../../docs/importing-into-devici.md).
- [Components and data flow](components.md): every element, its role, and its attributes
- [Threats](threats.md): curated threats by theme, with likelihood, severity, and risk
- [Threat details](threat-details.md): how each attack works and which mitigations counter it
- [Mitigation library](mitigation-library.md): every mitigation with implementation guidance, rationale, and examples

## At a glance

|  | Count |
|---|---|
| Curated threats documented here | 90 |
| Distinct mitigations | 142 |
| Threat-to-mitigation mappings | 306 |
| Threats in the full importable model | 148 |

The documentation covers the curated set we scored and prioritized. The importable model also includes every additional threat mapped to its components.

| Risk level | Threats |
|---|---|
| Critical | 15 |
| High | 41 |
| Medium | 15 |
| Low | 2 |
| Unrated | 17 |

| Control type | Mitigations |
|---|---|
| Preventive | 114 |
| Detective | 25 |
| Corrective | 3 |

## System summary

This model represents a Large Language Model (LLM) system interacting with clients, automation agents, and various data stores.
- Core Flow: Users (and potential attackers) interact via Application Services, which route requests to an LLM Production Environment.
- Orchestration: Automation Agents coordinate user prompts and system instructions before they reach the LLM Model.
- Data Support: The model is supported by Training/Fine-tuning Data, RAG (Retrieval-Augmented Generation) Data Stores, and Vector Databases for context.
- Execution: The model can trigger Server-Side Functions to execute logic or integrate with non-LLM systems.
- External Sources: Data is ingested from External Data Sources (public and proprietary) which are explicitly treated as untrusted.

## Scope

In-Scope: The logical data flow from the client to the model, the interaction with supporting data structures (RAG, Vector DB), and the integration with server-side functions.

Out-of-Scope: Specific hosting platforms (AWS, Azure, etc.), API endpoint implementation details, and container orchestration tools.

## Assumptions

Application Services successfully handle standard authentication and authorization before the LLM processes requests.

The "External Data Sources" are inherently untrusted and pose a risk of data poisoning or injection.

Cloud infrastructure provides a baseline of scalability and isolation for the Vector DB and RAG stores.
