# Medical Device: Review Notes

An honest review of this reference model: what it covers well and where it falls short. Use it as a checklist when adapting the model to your own system. Back to the [model overview](README.md).

## Model elements

Based on standard architectural patterns for medical IoT (IoMT) systems, there are several elements that appear to be missing (creating blind spots) and a few that are extraneous (or redundant).

1. Missing Elements (Critical Gaps)

These are standard components that likely exist in reality but are missing from the diagram. Without them, some specific high-risk threats would be missed.

| Missing Element | Why it is Critical |
|---|---|
| Identity Provider (IdP) | High Criticality. The diagram shows a "Gateway" but no component for verifying who the users are (e.g., Auth0, Cognito, Active Directory). You cannot model threats like Token Theft or Session Hijacking without an Auth service. |
| Key Management / HSM | High Criticality. Medical data must be encrypted. Where are the keys? A specific "Key Store" or "HSM" (Hardware Security Module) element is needed to model risks like Hardcoded Keys or Key Extraction. |
| Bluetooth/Network Interface | Medium Criticality. Inside the "Medical Device," the "Operating System" is too broad. You need a specific "Network Interface" element (e.g., BLE Radio) to model Blueborne attacks or Pairing bypasses. |
| Admin/Support Interface | Medium Criticality. Who fixes the system? There is usually a "SysAdmin" or "Support" actor who has elevated privileges. These accounts are often the primary target for attackers to gain "God Mode" access. |

Extraneous or Redundant Elements

These elements effectively duplicate other parts of the model or represent data flows as static objects.

| Element | Critique |
|---|---|
| "Sensor Data" (Store) | Redundant. "Sensor Data" is typically a flow of information, not a static data store element, unless the device has a significant buffer. Modeling it as a separate store inside the device often leads to double-counting threats that strictly belong to the "Health Controller." |
| "Updated Medical App" | Confusing. This is an object, but it represents a state change. It is clearer to model the "App Store" simply as an external entity that sends a "Binary Update" data flow. You don't need a separate bubble for the updated app itself. |

## Threats

2. Gaps (What is missing?)

Missing threats specific to the local connectivity protocols and the actuation feedback loop.

A. The description states the device "communicates directly" with the phone. This usually implies Bluetooth Low Energy (BLE) or NFC, which is not specified.

B. The "Feedback Loop" (Command & Control)

The model mentions "feedback or updates return to the patient." If this feedback controls the device (e.g., "Change settings," "Start therapy"), the current list is too generic.

- Command Replay Attack: An attacker records a valid "Start Therapy" command sent by the cloud and replays it later to overdose the patient.

- Lack of Command Atomicity: If a command is interrupted (e.g., phone battery dies mid-update), does the device fail-safe or hang in an undefined state?

C. Cloud Segmentation

The model separated "Service Data" (User-side) from "Medical Data" (Clinician-side).

- Cross-Repository Contamination: A threat where an API logic flaw allows a user in the "Patient Portal" to accidentally query the "Medical Data" tables directly (bypassing the clinician view).

- Insider Threat (Clinician): The list mentions "Broken Access Control," but misses the specific threat of a Malicious Insider (e.g., a nurse or admin) misusing valid credentials to view records of high-profile patients.

## Recommendations to Close the Gaps

| New Threat Title | Framework | Why it is needed |
|---|---|---|
| Bluetooth Low Energy (BLE) MITM | Mobile / IoT | Addresses the specific risk of the local link between Device and Phone. |
| Command Replay Attack | STRIDE | Specific to the "Feedback" loop; ensures old commands cannot be re-sent to trigger therapy. |
| Fail-Safe State Failure | Safety | specific to the device disconnecting mid-update or mid-command. |
| Clinician Insider Threat | Operational | Addresses the risk of authorized hospital staff abusing access to the "Medical Data" repository. |
