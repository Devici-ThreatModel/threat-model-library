# Mobile App Reference Threat Model

A mobile app running in its OS sandbox: UI, application logic, local storage, and communication with backend and cloud services.

**Importable model:** [`mobile-app.otm.json`](mobile-app.otm.json)

## Scope

**In scope:** The app sandbox and its interfaces to the OS, user, and backend.

**Out of scope:** Backend internals and app-store infrastructure.

## Assumptions

The OS enforces sandboxing; users may install the app from official or unofficial channels.

## Known gaps

Add the standard mobile components relevant to your app (push notifications, deep links, SDKs) before relying on the model.

See [Importing into Devici](../../docs/importing-into-devici.md) to load this model.
