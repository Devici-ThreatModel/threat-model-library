# Threat Modeling Library

**Industry-specific reference threat models and best-practice guidance for threat modeling.**

Threat modeling is easier when you aren't starting from a blank canvas. This library is a collection of reference threat models for the systems teams actually build (web apps, mobile apps, LLM and agentic systems, IoT, automotive, and medical devices) alongside guidance on how to evaluate, organize, and prioritize what you find.

Each reference model has full written documentation (components, threats, mitigations, and review notes) plus CSV downloads alongside an importable file in Open Threat Model (OTM) format, containing components, data flows, trust boundaries, threats, and mitigations. Load them into [Devici](https://app.devici.com/sign-up) for free, or read the JSON directly.

> Published by [Devici](https://devici.com).

---

## Start in 5 minutes

1. **Sign up free:** <https://app.devici.com/sign-up>
2. **Pick a model** from the [catalog](#the-catalog) and download its `.otm.json` file.
3. **Import it:** in Devici, create a new threat model by importing an OTM file and select the file you downloaded. The diagram, threats, and mitigations appear on a canvas you own.
4. **Make it yours:** rename components to match your architecture, remove what doesn't apply, and add what's missing.

## The catalog

| Model | What it covers | Components | Threats | Mitigations |
|---|---|---|---|---|
| [**Web App**](models/web-app) | Service-based cloud web app: browser, CDN, API gateway, three services with per-service databases, IdP, central logging | 21 | 134 | 328 |
| [**Mobile App**](models/mobile-app) | App sandbox on the mobile OS: UI, app logic, local storage, backend and cloud communication | 15 | 58 | 122 |
| [**LLM and Agentic Systems**](models/llm-agentic-ai) | Users, agents, models, and external data across trust boundaries; prompt injection, excessive agency | 19 | 148 | 494 |
| [**IoT Device**](models/iot) | Smart air-quality system: sensors, on-device aggregation, cloud analytics, HVAC control, integration APIs | 18 | 113 | 279 |
| [**Automotive**](models/automotive) | Connected vehicle: infotainment, ECUs, CAN bus, ADAS, wireless interfaces | 35 | 38 | 92 |
| [**Medical Device**](models/medical-device) | Connected therapy device, patient phone app, gateway, clinician and patient data stores | 17 | 64 | 116 |

## Best-practice guides

- [**Evaluating a threat model**](docs/evaluating-a-threat-model.md): accuracy and completeness checks, and how to find gaps
- [**Organizing threats and mitigations**](docs/organizing-threats-and-mitigations.md): grouping, framework mapping, and priority scoring
- [**Importing into Devici**](docs/importing-into-devici.md): detailed steps and troubleshooting

## Repository layout

```
models/<industry>/
  <name>.otm.json        # importable model (OTM 0.2.0)
  README.md              # overview, priority summary, scope, assumptions
  components.md          # every component and data flow
  threats.md             # curated threats by theme, with priority levels and mitigations
  <name>-threats-and-mitigations.csv  # full descriptions and mitigation guidance
  <name>-components.csv  # components and data flow
  review-notes.md        # coverage gaps and refinements (where available)
docs/                 # best-practice guides
```

## License

Free to use, copy, modify, and share, including commercially, under the [MIT License](LICENSE).
