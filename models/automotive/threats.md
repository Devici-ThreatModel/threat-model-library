# Automotive: Threats

37 curated threats, grouped by theme and ordered by risk. Select a threat for its full description and mitigations. Back to the [model overview](README.md).

## Risk summary

| Risk level | Threats |
|---|---|
| Critical | 8 |
| High | 20 |
| Medium | 7 |
| Low | 2 |

## Vehicle Control & Safety Critical (CAN Bus & ECUs)

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Braking & Safety ECU Command Suppression / Safety System Disablement](threat-details.md#braking--safety-ecu-command-suppression--safety-system-disablement) | STRIDE: Denial of Service | Low | Critical | **Critical** | Prevent brakes or airbags from deploying during an emergency. |
| [ECU impersonation / spoofing](threat-details.md#ecu-impersonation--spoofing) | STRIDE: Spoofing | Medium | Critical | **Critical** | A compromised non-critical ECU (e.g., Radio) pretends to be the Safety ECU to send fake commands. |
| [Gateway or bridge compromise](threat-details.md#gateway-or-bridge-compromise) | STRIDE: Elevation of Privilege | Medium | Critical | **Critical** | The "Holy Grail" attack: Breaking the segmentation between Infotainment and CAN Bus. |
| [Lateral movement to CAN or vehicle control networks](threat-details.md#lateral-movement-to-can-or-vehicle-control-networks) | STRIDE: Elevation of Privilege | Medium | Critical | **Critical** | Moving from a compromised Wifi/Bluetooth entry point into the safety network. |
| [ADAS Sensor Manipulation / Assistance System Degradation](threat-details.md#adas-sensor-manipulation--assistance-system-degradation) | STRIDE: Tampering | Medium | Critical | **High** | Cause the vehicle to ignore obstacles or brake unnecessarily (phantom braking). |
| [Bus flooding / Denial-of-service (DoS)](threat-details.md#bus-flooding--denial-of-service-dos) | STRIDE: Denial of Service | Medium | High | **High** | Flood the CAN bus to freeze ECU communications; vehicle enters "limp mode" or shuts down. |
| [Diagnostic interface exploitation (OBD-II, UDS)](threat-details.md#diagnostic-interface-exploitation-obd-ii-uds) | STRIDE: Elevation of Privilege | High | High | **High** | Bypass authentication to inject CAN messages via physical port (Key cloning, theft). |
| [ECU firmware manipulation or reflashing](threat-details.md#ecu-firmware-manipulation-or-reflashing) | STRIDE: Tampering | Low | Critical | **High** | Permanently alter vehicle behavior, remove speed limiters, or disable safety features. |
| [Engine & Powertrain ECU Overload / Destructive DoS](threat-details.md#engine--powertrain-ecu-overload--destructive-dos) | STRIDE: Denial of Service | Low | Critical | **High** | Cause physical damage to the engine (overheating, over-revving) via repeated commands. |
| [Exploiting insecure bootloaders](threat-details.md#exploiting-insecure-bootloaders) | STRIDE: Tampering | Low | Critical | **High** | Bypass trust chain to load malicious OS or firmware on ECUs. |
| [Memory corruption or buffer overflow in ECU software](threat-details.md#memory-corruption-or-buffer-overflow-in-ecu-software) | CWE / STRIDE: Tampering | Medium | High | **High** | Crash an ECU or execute arbitrary code via malformed packets. |
| [Replay attacks on CAN traffic](threat-details.md#replay-attacks-on-can-traffic) | STRIDE: Spoofing | High | Medium | **High** | Capture and re-send valid commands (e.g., "Unlock Door") to trigger actions without auth. |
| [Unauthorized CAN message injection](threat-details.md#unauthorized-can-message-injection) | STRIDE: Tampering | Low | Critical | **High** | Send fabricated messages to control steering, acceleration, or braking. |
| [Key or credential leakage from ECUs](threat-details.md#key-or-credential-leakage-from-ecus) | STRIDE: Info Disclosure | Low | High | **Medium** | Extract cryptographic keys to decrypt firmware or spoof valid messages. |

## Connectivity & Infotainment (Entry Points)

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Bluetooth exploitation](threat-details.md#bluetooth-exploitation) | STRIDE: Elevation of Privilege | High | Medium | **High** | Remote code execution or pairing without consent to access contacts or unlock the car. |
| [Compromised mobile app integrations (Android Auto / CarPlay)](threat-details.md#compromised-mobile-app-integrations-android-auto--carplay) | STRIDE: Spoofing | High | Medium | **High** | Use a compromised phone to send malicious input to the head unit. |
| [Security Misconfiguration (Web and Mobile)](threat-details.md#security-misconfiguration-web-and-mobile) | OWASP: Security Misconfig | High | High | **High** | Default passwords or open debug ports left on the Infotainment OS. |
| [Client-Side Injection](threat-details.md#client-side-injection) | OWASP: Injection | High | Low | **Medium** | Execute malicious scripts in the Infotainment browser/UI. |
| [Malicious USB device injection](threat-details.md#malicious-usb-device-injection) | STRIDE: Tampering | Medium | Medium | **Medium** | Fuzzing the USB stack to crash the Infotainment OS or gain shell access. |
| [Voice-assistant command injection](threat-details.md#voice-assistant-command-injection) | STRIDE: Tampering | Medium | Medium | **Medium** | Using hidden audio frequencies or recorded voice to trigger commands (e.g., "Open Garage"). |
| [Session Hijacking](threat-details.md#session-hijacking) | OWASP: Broken Access Control | Medium | Low | **Low** | Taking over an active user session (e.g., Spotify or Navigation) to steal data. |
| [Side-channel data leakage](threat-details.md#side-channel-data-leakage) | STRIDE: Info Disclosure | Low | High | **Low** | Analyzing power consumption or EM emissions to deduce crypto keys (very advanced). |

## Software Lifecycle, Backend & Privacy

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Broken Authentication](threat-details.md#broken-authentication) | OWASP: Identification Failures | High | High | **Critical** | Weak passwords allowing attackers to log into the vehicle mobile app/account. |
| [Exploiting legacy or unsupported firmware](threat-details.md#exploiting-legacy-or-unsupported-firmware) | OWASP: Vulnerable Components | High | High | **Critical** | Attacking known vulnerabilities in old libraries (e.g., old Linux kernel in Infotainment). |
| [Hijacked OTA (Over-the-Air) update mechanisms](threat-details.md#hijacked-ota-over-the-air-update-mechanisms) | STRIDE: Tampering | Low | Critical | **Critical** | Pushing a malicious firmware update to the entire fleet of vehicles. |
| [Insecure Data Storage](threat-details.md#insecure-data-storage) | OWASP Mobile: Insecure Storage | High | High | **Critical** | Storing tokens or keys in plaintext on the Infotainment file system. |
| [Broken access control](threat-details.md#broken-access-control) | OWASP: Broken Access Control | Medium | High | **High** | User A accessing User B's vehicle telemetry or location data. |
| [Cryptographic failure](threat-details.md#cryptographic-failure) | OWASP: Crypto Failures | Low | Critical | **High** | Weak encryption enabling decryption of OTA updates or stored user data. |
| [Data Disclosure](threat-details.md#data-disclosure) | LINDDUN: Identifiability | High | Medium | **High** | Leaking GPS history or PII (Personally Identifiable Information) to unauthorized parties. |
| [Exploiting unpatched software vulnerabilities](threat-details.md#exploiting-unpatched-software-vulnerabilities) | OWASP: Vulnerable Components | Medium | High | **High** | Zero-day attacks on the OS or 3rd party libraries. |
| [Insecure Inter-Process Communication (IPC)](threat-details.md#insecure-inter-process-communication-ipc) | STRIDE: Elevation of Privilege | Medium | High | **High** | malicious app on Infotainment talking to the Gateway service without permission. |
| [Insufficient Transport Layer Protection](threat-details.md#insufficient-transport-layer-protection) | OWASP: Crypto Failures | Medium | High | **High** | Sending telemetry or commands over HTTP instead of HTTPS (Man-in-the-Middle). |
| [Vulnerable and Outdated Components](threat-details.md#vulnerable-and-outdated-components) | OWASP: Vulnerable Components | High | High | **High** | Using libraries with known CVEs (Common Vulnerabilities and Exposures). |
| [Weak Server-Side Controls](threat-details.md#weak-server-side-controls) | OWASP API: Broken Object Level Auth | Medium | Critical | **High** | Backend API allowing unverified commands to be sent to the vehicle. |
| [Insecure Communication with Third-Party Services](threat-details.md#insecure-communication-with-third-party-services) | OWASP API: Unsafe Consumption | High | Low | **Medium** | Intercepting data sent between the car and music/weather services. |
| [Malicious Code and Malware](threat-details.md#malicious-code-and-malware) | STRIDE: Tampering | Medium | Medium | **Medium** | Ransomware locking the infotainment screen until payment is made. |
| [Reverse Engineering](threat-details.md#reverse-engineering) | STRIDE: Info Disclosure | High | Low | **Medium** | Analyzing app binaries to find API keys or logic flaws. |
