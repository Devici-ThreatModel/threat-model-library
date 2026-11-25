# Automotive: Standards Mapping

An indicative mapping of each threat to the automotive standards a reviewer is likely to be asked about. It supports a team that has to build a TARA or type-approval evidence from this model. It is **not** a TARA and not a compliance determination. Confirm each entry against the regulation text before using it as evidence. Back to the [model overview](README.md).

## What the model does and does not carry

| Standard | What the model offers | What it does not offer |
|---|---|---|
| ISO/SAE 21434 | Threats, attack paths and priorities that can feed a TARA, with an indicative impact category per threat | Attack feasibility ratings and calculated risk values |
| UN Regulation No. 155 | Threats grouped by theme, and 9 detective controls for the detect-and-respond expectation | A cybersecurity management system or audit evidence |
| UN Regulation No. 156 | The update-related threats flagged below, each with mitigations | A software update management system |
| ISO 26262 | Threats that reach braking, steering and driver assistance | ASIL ratings |

## Mapping

Impact category uses the ISO/SAE 21434 categories: **S** safety, **F** financial, **O** operational, **P** privacy. The R155 theme is the matching high-level threat category in the regulation's Annex 5, Part A. R156 marks threats that bear on update integrity and authenticity (Yes, or Indirect where the threat undermines the keys that update verification depends on).

| Threat | Impact | R155 theme | R156 |
|---|---|---|---|
| Braking & Safety ECU Command Suppression / Safety System Disablement | S | Communication channels | |
| ECU impersonation / spoofing | S | Communication channels | |
| Gateway or bridge compromise | S | Communication channels | |
| Lateral movement to CAN or vehicle control networks | S | External connectivity | |
| ADAS Sensor Manipulation / Assistance System Degradation | S | Hardening and vulnerabilities | |
| Bus flooding / Denial-of-service (DoS) | S, O | Communication channels | |
| Diagnostic interface exploitation (OBD-II, UDS) | S, F | External connectivity | |
| ECU firmware manipulation or reflashing | S, F | Update process | Yes |
| Engine & Powertrain ECU Overload / Destructive DoS | S, F | Communication channels | |
| Exploiting insecure bootloaders | S | Update process | Yes |
| Memory corruption or buffer overflow in ECU software | S | Hardening and vulnerabilities | |
| Replay attacks on CAN traffic | S | Communication channels | |
| Unauthorized CAN message injection | S | Communication channels | |
| Key or credential leakage from ECUs | S, F | Data and code protection | Indirect |
| Bluetooth exploitation | O, P | External connectivity | |
| Compromised mobile app integrations (Android Auto / CarPlay) | O, P | External connectivity | |
| Security Misconfiguration (Web and Mobile) | O | Hardening and vulnerabilities | |
| Keyless entry relay and replay attacks | F | External connectivity | |
| Client-Side Injection | O | Hardening and vulnerabilities | |
| Voice-assistant command injection | O, P | External connectivity | |
| Malicious USB device injection | O | External connectivity | |
| Session Hijacking | P | External connectivity | |
| Side-channel data leakage | F | Data and code protection | |
| Broken Authentication | P, F | Back-end servers | |
| Exploiting legacy or unsupported firmware | S, O | Update process | Yes |
| Hijacked OTA (Over-the-Air) update mechanisms | S, F, O | Update process | Yes |
| Insecure Data Storage | P | Data and code protection | |
| Broken access control | P | Back-end servers | |
| Cryptographic failure | P, F | Data and code protection | Indirect |
| Data Disclosure | P | Data and code protection | |
| Exploiting unpatched software vulnerabilities | S, O | Update process | Yes |
| Insecure Inter-Process Communication (IPC) | O | Hardening and vulnerabilities | |
| Insufficient Transport Layer Protection | P | Communication channels | |
| Vulnerable and Outdated Components | O | Hardening and vulnerabilities | Indirect |
| Weak Server-Side Controls | S, F | Back-end servers | |
| Insecure Communication with Third-Party Services | P | Communication channels | |
| Malicious Code and Malware | O, F | Unintended human actions | |
| Reverse Engineering | F | Data and code protection | |
| HSM compromise or misuse of key operations | S, F | Data and code protection | Indirect |

## Next steps for a team that needs a TARA

1. Take the threats with an **S** impact and assign each an ASIL-linked severity with your safety team.
2. Rate attack feasibility for each path in [attack-paths.md](attack-paths.md), using your own attacker model.
3. Carry the result into your own risk values. This model's priority is expert judgment, not a calculated risk value.
