# Automotive: Review Notes

An honest review of this reference model: what version 2 fixed, where it still falls short, and how it scores against the scorecard in the guide *How to Review an Automotive Threat Model*. Use it as a checklist when adapting the model to your own system. Back to the [model overview](README.md).

## Gaps from version 1, now drawn

Version 1's review named four hardware realities the architecture left out. Version 2 draws each one and attaches threats to it.

1. **The OBD-II port.** Now an OBD-II Port and a Diagnostic Tool or Aftermarket Dongle, connected to the Central Gateway ECU. The diagnostic interface, CAN injection, and firmware reflashing threats now attach to the port. A laptop plugged into the car is a path the model can show. See [attack path 3](attack-paths.md).
2. **The secure gateway.** Now a Central Gateway ECU between the onboard computer and the CAN bus. All five ECU data flows run through it, so segmentation can be analyzed. Gateway compromise, lateral movement, and bus flooding attach to it.
3. **The hardware security module.** Now an HSM in the computing system, connected to the Infotainment OS and the onboard computer. Key leakage, OTA hijacking, insecure bootloaders, and side-channel threats attach to it, and a new threat covers compromise or misuse of the HSM itself.
4. **The keyless entry receiver.** Now a Keyless Entry Receiver and a Key Fob feeding the Body & Comfort Systems ECU, with a new threat for relay and replay attacks. See [attack path 4](attack-paths.md).

## Still missing

- **Cellular telematics unit, V2X communication, and EV charging.** None is drawn. A model for a specific vehicle needs them.
- **Security modules embedded in individual ECUs.** The HSM is modeled once, in the computing system.
- **TARA values and ASIL ratings.** Priority is expert judgment, and no ISO 26262 safety levels are assigned. See the [standards mapping](standards-mapping.md).

## Mitigations

Version 2 replaced the filler, mismatched, and duplicate mitigations from version 1 with ones that name a component and a mechanism. Examples: *Harden Assets Against Attacks* and *Implement Timely Patching* on security misconfiguration, *Audit Logging Configuration* on side-channel leakage, *Develop a comprehensive threat model* on two threats, and the duplicate *Implement access control mechanisms*. It also added detective and corrective controls, so every Critical threat now has at least one.

Some mitigations imported from the Devici library are still generic, for example *Validate User Input*, *Implement Parameterization*, *Map all authentication flows*, *Classify data sensitivity*, and *Use Trusted Frameworks*. They give good coverage, and a team adapting the model should rewrite them to name its own component and mechanism.

## Scorecard

Scored with the guide's rubric: a criterion rates Strong when every item is true, Adequate when one is false, and Weak when two or more are false.

| Criterion | Item | Result | Note |
|---|---|---|---|
| Accuracy | Every threat names an affected component that exists in the architecture | True | Gateway and diagnostic threats now attach to drawn components |
| Accuracy | Priorities agree with the attacker's goal, and the model says how it set them | True | The README states that priority is expert judgment |
| Accuracy | Each threat sits under a framework that fits it | True | GPS and personal data leakage sits under LINDDUN |
| Accuracy | Threats connect into attack paths from each entry point | True | Eight paths in [attack-paths.md](attack-paths.md), including the phone integration and the voice assistant |
| Completeness | Physical access points appear in the diagram | True | USB, OBD-II port, keyless entry receiver |
| Completeness | The secure gateway is drawn as its own component | True | Central Gateway ECU, between the computing and CAN boundaries |
| Completeness | A hardware security module appears wherever updates and keys are discussed | True | One HSM in the computing system; ECU-embedded modules are not drawn |
| Completeness | At least one threat tests each stated assumption | True | Gateway compromise tests the first, hijacked OTA the second |
| Completeness | The model maps to the standards your auditors use | False | Indicative mapping only, no TARA values or ASIL ratings |
| Specificity | Each mitigation names its component and its mechanism | False | Library mitigations listed above remain generic |
| Specificity | The mix of control types matches the exposure | True | Every Critical threat has a detective or corrective control, though 74 of 90 mitigations are preventive |
| Specificity | No mitigation is filler, and no two say the same thing | True | The LINDDUN entries on Data Disclosure overlap in places |

**Result: Accuracy Strong, Completeness Adequate, Specificity Adequate.**
