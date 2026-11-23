# LLM and Agentic Systems Reference Threat Model

How an LLM-based system moves data between users, agents, models, and external sources across trust boundaries, including retrieval, tool use, and autonomous agents.

**Importable model:** [`llm.otm.json`](llm.otm.json)

## Scope

**In scope:** Application services, agent automation, model interaction, and external data and tool sources.

**Out of scope:** Model training infrastructure and provider internals.

## Assumptions

Untrusted content can reach the model through users and external sources.

## Known gaps

Tailor agent permissions, tool inventories, and memory stores to your design.

See [Importing into Devici](../../docs/importing-into-devici.md) to load this model.
