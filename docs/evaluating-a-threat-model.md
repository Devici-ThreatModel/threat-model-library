# Evaluating a Threat Model

A threat model that looks thorough can still be wrong or incomplete. Review every model against two questions, as we do for each reference model in this library.

## 1. Accuracy: are the threats we listed real and well-formed?

For each threat, check:

- **Is it plausible for this architecture?** A threat should name the component or data flow it applies to. If you can't point to where it happens, it's generic noise.
- **Is the attacker goal stated?** "Cause the vehicle to ignore obstacles" is a goal. "ADAS issue" is not.
- **Are likelihood and severity defensible?** Ask who the attacker is, what access they need, and what the worst realistic outcome is. In safety-critical systems (automotive, medical), severity is anchored to harm to people, not just data loss.
- **Is it mapped to a recognized framework?** STRIDE, OWASP Top 10, OWASP API Top 10, OWASP LLM Top 10, and MAESTRO appear across the reference models. Mapping makes threats comparable and auditable.

## 2. Completeness: what did we miss?

Look for gaps in three places.

### Missing components
Ask what a real deployment of this system has that the diagram doesn't. Reviews of the reference models repeatedly find:

| Commonly missing | Why it matters |
|---|---|
| Identity provider | Without it you can't model token theft or session hijacking |
| Key management / HSM | Needed to model hardcoded keys and key extraction |
| Network or radio interface (BLE, Wi-Fi) | An "operating system" box is too coarse to model pairing bypass or protocol attacks |
| Admin and support actors | Privileged operators are a prime target |
| Logging and monitoring | Needed for repudiation and detection threats |

### Redundant components
Watch for elements that double-count threats, such as a data *flow* modeled as a data *store*, or a state change (an "updated app") modeled as its own object.

### Missing threats
Walk the data flows and trust boundaries and ask which classic categories are absent. For example, the Web App model lacks explicit missing injection, XSS, CSRF, cryptographic failures, and clickjacking. The Medical Device model lacks command replay, fail-safe failure on interrupted updates, and clinician insider abuse.

## A quick review checklist

- [ ] Scope and out-of-scope are written down
- [ ] Assumptions are explicit (for example, "the cloud provider handles physical security")
- [ ] Every trust boundary crossing has at least one data flow and one threat
- [ ] Every high or critical threat has at least one mitigation
- [ ] Each mitigation says *how* to implement it, not just what to call it
- [ ] Known gaps are recorded, not hidden
