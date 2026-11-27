# Automotive: Attack Paths

The threats in [threats.md](threats.md) are separate entries. This page reads them in order, from an entry point to an impact, for each entry point the model names. Priorities are from the threat tables. Back to the [model overview](README.md).

## 1. Bluetooth to the safety network

| Step | Threat | Priority | Component |
|---|---|---|---|
| 1 | Bluetooth exploitation | High | Bluetooth Controller |
| 2 | Lateral movement to CAN or vehicle control networks | Critical | Infotainment OS, Central Gateway ECU |
| 3 | Gateway or bridge compromise | Critical | Central Gateway ECU |
| 4 | ECU impersonation / spoofing, or Unauthorized CAN message injection | Critical, High | CAN Bus |

Impact: fake commands to the Braking & Safety ECU. The gateway is the control that appears at every step after the first.

## 2. USB to the safety network

| Step | Threat | Priority | Component |
|---|---|---|---|
| 1 | Malicious USB device injection | Medium | USB Controller |
| 2 | Exploiting unpatched software vulnerabilities, or Exploiting legacy or unsupported firmware | High, Critical | Infotainment OS |
| 3 | Lateral movement to CAN or vehicle control networks | Critical | Infotainment OS, Central Gateway ECU |
| 4 | Gateway or bridge compromise | Critical | Central Gateway ECU |

Impact: same as path 1. A weak first step does not mean a low-impact path, so read the whole chain.

## 3. OBD-II port to the CAN bus

| Step | Threat | Priority | Component |
|---|---|---|---|
| 1 | Diagnostic interface exploitation (OBD-II, UDS) | High | OBD-II Port, Central Gateway ECU |
| 2 | Unauthorized CAN message injection | High | CAN Bus, OBD-II Port |
| 3 | ECU firmware manipulation or reflashing | High | CAN Bus, OBD-II Port |

Impact: key cloning, vehicle theft, altered vehicle behavior. This is the shorter route that version 1 could not show. The gateway's diagnostic filtering is the main control.

## 4. Key fob to vehicle theft

| Step | Threat | Priority | Component |
|---|---|---|---|
| 1 | Keyless entry relay and replay attacks | High | Keyless Entry Receiver |
| 2 | Diagnostic interface exploitation (OBD-II, UDS), once inside the car | High | OBD-II Port |

Impact: the vehicle is unlocked, started or programmed with a new key. The immobilizer check between the Body & Comfort ECU and the Engine ECU limits what a successful relay achieves.

## 5. Wi-Fi and the manufacturer backend to the fleet

| Step | Threat | Priority | Component |
|---|---|---|---|
| 1 | Insufficient Transport Layer Protection, or Insecure Communication with Third-Party Services | High, Medium | Infotainment OS |
| 2 | Hijacked OTA (Over-the-Air) update mechanisms | Critical | Infotainment OS, Hardware Security Module (HSM) |
| 3 | HSM compromise or misuse of key operations | High | Hardware Security Module (HSM) |
| 4 | ECU firmware manipulation or reflashing | High | CAN Bus, OBD-II Port |

Impact: a malicious update to many vehicles at once. Signed OTA packages and the HSM that verifies them are the controls that matter, and the rollback and staged rollout limit how far a bad package spreads.

## 6. Owner account to remote commands

| Step | Threat | Priority | Component |
|---|---|---|---|
| 1 | Broken Authentication | Critical | Infotainment OS |
| 2 | Weak Server-Side Controls | High | Infotainment OS |
| 3 | Broken access control | High | Infotainment OS |

Impact: unauthorized remote commands and exposure of another owner's location data.

## 7. Phone integration to the safety network

| Step | Threat | Priority | Component |
|---|---|---|---|
| 1 | Compromised mobile app integrations (Android Auto / CarPlay) | High | Infotainment OS |
| 2 | Exploiting unpatched software vulnerabilities | High | Infotainment OS |
| 3 | Lateral movement to CAN or vehicle control networks | Critical | Infotainment OS, Central Gateway ECU |
| 4 | Gateway or bridge compromise | Critical | Central Gateway ECU |

Impact: same as paths 1 and 2. A compromised phone reaches the head unit over USB or Bluetooth, so this path shares its later steps with those two. It is listed separately because the first step is the phone and its apps, not the radio or the port.

## 8. Voice assistant to unwanted commands

| Step | Threat | Priority | Component |
|---|---|---|---|
| 1 | Voice-assistant command injection | Medium | Infotainment OS |
| 2 | Lateral movement to CAN or vehicle control networks, only if the head unit is also compromised | Critical | Infotainment OS, Central Gateway ECU |

Impact: unwanted commands issued through the assistant, such as opening a garage door. Reaching vehicle control needs a second weakness in the head unit, and the gateway filtering is the control that limits it. User-verified actions are the main control on step 1.
