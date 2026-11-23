# Web Application Reference Threat Model

A cloud-hosted, service-oriented web app serving external users through a browser, with a CDN for static assets and an API gateway in front of three services (content/domain data, user profile/account, authentication/authorization), a database per service, an identity provider for MFA, and a centralized logging service.

**Importable model:** [`web-app.otm.json`](web-app.otm.json)

## Scope

**In scope:** The application layer, API gateway, the three services and their databases, and client-side browser interaction.

**Out of scope:** Underlying cloud infrastructure and the internals of managed services such as the CDN and IdP.

## Assumptions

The cloud provider supplies a secure baseline; the IdP handles MFA and token cryptography securely; service-to-service traffic stays on a private network.

## Known gaps

Injection from the browser, XSS, CSRF, cryptographic failures, and clickjacking are not modeled explicitly; add them for your own system.

See [Importing into Devici](../../docs/importing-into-devici.md) to load this model.
