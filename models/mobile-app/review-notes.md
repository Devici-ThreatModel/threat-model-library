# Mobile App: Review Notes

An honest review of this reference model: what it covers well and where it falls short. Use it as a checklist when adapting the model to your own system. Back to the [model overview](README.md).

## Elements in the Model

1. Missing Elements (Standard Mobile App Components)

To make this a complete reference model for a modern mobile application, the following elements are commonly part of the ecosystem and represent distinct threat vectors:

- Push Notification Services (APNS / FCM):
    - Why: Almost all modern apps receive asynchronous alerts (e.g., "New Message," "Update Available").
    - Threat: Notification spoofing or data leakage via lock screen previews.
- Analytics & Crash Reporting (e.g., Firebase, Sentry):
    - Why: Apps automatically send usage and crash logs to third-party collectors.
    - Threat: Inadvertent leakage of PII or sensitive tokens in crash dumps.
- Deep Links / Custom URL Schemes:
    - Why: The diagram shows "User Interface" as the only entry point. In reality, the OS triggers the app via links (e.g., myapp://reset-password).
    - Threat: This is a massive attack surface for parameter injection and logic bypass (often used in the "App Proxy Attack" you listed earlier).
- WebView:
    - Why: If your app displays any web content (Help pages, Terms of Service, or hybrid screens), a WebView element must be modeled inside the sandbox.
    - Threat: Cross-Site Scripting (XSS) and Bridge access attacks.

2. Logic Flow Refinements

OAuth 2.0 Callback Flow:

Current: Arrow points from "OAuth 2.0" -> "Application Logic."

Refinement: Technically, the Identity Provider (IdP) redirects the User's Browser, which then calls the Mobile OS (via Deep Link), which then opens the App.

Correction: If you want high fidelity, ensure the "Deep Link" entry point is added to the OS boundary to handle this callback.

| Element | Status | Action Required |
|---|---|---|
| Push Notifications | Missing | Add External Entity (APNS/FCM) + Flow to OS. |
| Telemetry/Analytics | Missing | Add External Entity + Flow from App Logic. |
| Deep Links (Intents) | Missing | Add entry point from "Mobile OS" to "App Logic." |

## Threats

| Missing Threat | Target Element | Why it matters |
|---|---|---|
| Deep Link Hijacking | Mobile OS / IPC | "Insecure IPC" is vague; this is a primary vector for token theft. |
| Overlay / Tapjacking | User Interface | A common Android malware technique that generic "Tampering" misses. |
