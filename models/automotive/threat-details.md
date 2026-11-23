# Automotive: Threat Details

For each threat: how the attack works, what it affects, and which mitigations counter it. Mitigation names link to the [mitigation library](mitigation-library.md). Back to the [threat list](threats.md) or the [model overview](README.md).

## Vehicle Control & Safety Critical (CAN Bus & ECUs)

### Braking & Safety ECU Command Suppression / Safety System Disablement

**Priority:** Critical · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE: Denial of Service

**Affects:** Braking & Safety ECU

An attacker with access to the vehicle’s internal networks (through compromised infotainment, telematics, OBD-II, or a breached gateway ECU) can inject spoofed or high-priority CAN frames that override or suppress legitimate braking, ABS, ESC, or airbag control messages. Because many braking and safety ECUs rely on unauthenticated, real-time CAN traffic, the attacker can block critical sensor inputs, disable actuator commands, or send false states that trick the system into thinking conditions are normal. This can result in brakes failing to engage, airbags failing to deploy during a crash, or safety interventions (ABS/ESC) being silently disabled. The outcome is direct compromise of occupant safety with high risk of injury or fatality.

**Attacker goal / impact:** Prevent brakes or airbags from deploying during an emergency.

**Mitigations**

- [Hardware-Enforced Safety Overrides and Fail-Safe Operating Modes](mitigation-library.md#hardware-enforced-safety-overrides-and-fail-safe-operating-modes) (Corrective)
- [Secure Gateway Filtering With Safety-Critical Message Authentication](mitigation-library.md#secure-gateway-filtering-with-safety-critical-message-authentication) (Preventive)

### ECU impersonation / spoofing

**Priority:** Critical · **Likelihood:** Medium · **Severity:** Critical · **Framework:** STRIDE: Spoofing

**Affects:** CAN Bus

A malicious device attached to the CAN network can masquerade as a legitimate ECU. It can send control commands or respond to queries to mislead other modules. Without message authentication, the vehicle cannot differentiate between genuine and fake ECUs.

**Attacker goal / impact:** A compromised non-critical ECU (e.g., Radio) pretends to be the Safety ECU to send fake commands.

**Mitigations**

- [ECU Identity Verification With Message Authentication and Secure Gateways](mitigation-library.md#ecu-identity-verification-with-message-authentication-and-secure-gateways) (Preventive)
- [Segmented Network Architecture With ECU Whitelisting and ID Filtering](mitigation-library.md#segmented-network-architecture-with-ecu-whitelisting-and-id-filtering) (Preventive)

### Gateway or bridge compromise

**Priority:** Critical · **Likelihood:** Medium · **Severity:** Critical · **Framework:** STRIDE: Elevation of Privilege

**Affects:** CAN Bus

Modern vehicles use central gateways to isolate CAN subnets (powertrain, chassis, body). A compromised gateway ECU can bridge malicious messages across domains. This allows attackers to escalate from infotainment or telematics systems into safety-critical networks.

**Attacker goal / impact:** The "Holy Grail" attack: Breaking the segmentation between Infotainment and CAN Bus.

**Mitigations**

- [Hardened Gateway ECUs With Domain Isolation and Message Authentication](mitigation-library.md#hardened-gateway-ecus-with-domain-isolation-and-message-authentication) (Preventive)
- [Secure Gateway Firmware, Access Controls, and Continuous Monitoring](mitigation-library.md#secure-gateway-firmware-access-controls-and-continuous-monitoring) (Detective)

### Lateral movement to CAN or vehicle control networks

**Priority:** Critical · **Likelihood:** Medium · **Severity:** Critical · **Framework:** STRIDE: Elevation of Privilege

**Affects:** Infotainment OS

If the infotainment system shares a bridge or gateway with the vehicle’s CAN bus, a compromise may spread to safety-critical ECUs. This allows attackers to manipulate braking, steering, or sensor systems indirectly. Network segmentation flaws greatly amplify this risk.

**Attacker goal / impact:** Moving from a compromised Wifi/Bluetooth entry point into the safety network.

**Mitigations**

- [Secure Gateway Enforcement With Anomaly Detection and Access Controls](mitigation-library.md#secure-gateway-enforcement-with-anomaly-detection-and-access-controls) (Detective)
- [Strong Network Segmentation With Isolated Safety-Critical Domains](mitigation-library.md#strong-network-segmentation-with-isolated-safety-critical-domains) (Preventive)

### ADAS Sensor Manipulation / Assistance System Degradation

**Priority:** High · **Likelihood:** Medium · **Severity:** Critical · **Framework:** STRIDE: Tampering

**Affects:** Lane keeping, adaptive cruise control, and parking sensors

An attacker who compromises vehicle networks or ADAS sensor inputs (camera, radar, ultrasonic, or LiDAR) can disrupt or falsify data fed into the Advanced Driver Assistance ECU. By injecting spoofed CAN messages, jamming or blinding sensors, or suppressing perception data, the attacker can cause lane-keeping systems to drift, adaptive cruise control to misjudge distance, or parking assistance to fail. Since ADAS depends on real-time, accurate sensor fusion, these manipulations can disable lane guidance, create unsafe following behavior, or cause the ECU to ignore obstacles. In extreme cases, the system may apply incorrect steering, braking, or acceleration, putting occupants and bystanders at risk.

**Attacker goal / impact:** Cause the vehicle to ignore obstacles or brake unnecessarily (phantom braking).

**Mitigations**

- [Fail-Safe ADAS Modes With Redundant Perception Paths](mitigation-library.md#fail-safe-adas-modes-with-redundant-perception-paths) (Corrective)
- [Sensor Fusion Validation and Secure ADAS Message Filtering](mitigation-library.md#sensor-fusion-validation-and-secure-adas-message-filtering) (Preventive)

### Bus flooding / Denial-of-service (DoS)

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** STRIDE: Denial of Service

**Affects:** CAN Bus

Attackers can flood the CAN bus with high-priority frames, monopolizing bandwidth and preventing legitimate traffic. This can disable safety-critical systems or cause unpredictable ECU behavior. The system may appear frozen or enter a fail-safe mode.

**Attacker goal / impact:** Flood the CAN bus to freeze ECU communications; vehicle enters "limp mode" or shuts down.

**Mitigations**

- [Rate-Limiting and Priority Enforcement at Secure Gateways](mitigation-library.md#rate-limiting-and-priority-enforcement-at-secure-gateways) (Preventive)
- [Segmented CAN Networks With DoS-Resilient Isolation](mitigation-library.md#segmented-can-networks-with-dos-resilient-isolation) (Preventive)

### Diagnostic interface exploitation (OBD-II, UDS)

**Priority:** High · **Likelihood:** High · **Severity:** High · **Framework:** STRIDE: Elevation of Privilege

**Affects:** CAN Bus

Standardized diagnostic protocols like UDS (Unified Diagnostic Services) allow access to memory, fault codes, and even firmware updates. If not properly restricted, attackers can use these interfaces to alter configurations or reprogram ECUs. Remote attacks are possible when the diagnostic stack is exposed via telematics or infotainment gateways.

**Attacker goal / impact:** Bypass authentication to inject CAN messages via physical port (Key cloning, theft).

**Mitigations**

- [Access-Controlled Diagnostic Modes With Strong Authentication](mitigation-library.md#access-controlled-diagnostic-modes-with-strong-authentication) (Preventive)
- [Gateway-Level Filtering and Segmentation of Diagnostic Traffic](mitigation-library.md#gateway-level-filtering-and-segmentation-of-diagnostic-traffic) (Preventive)

### ECU firmware manipulation or reflashing

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE: Tampering

**Affects:** CAN Bus

If attackers gain access to diagnostic ports or OTA update systems, they can overwrite ECU firmware. This may install persistent malware or modify control logic. Unsigned or poorly verified firmware updates make this attack feasible.

**Attacker goal / impact:** Permanently alter vehicle behavior, remove speed limiters, or disable safety features.

**Mitigations**

- [Cryptographically Signed Firmware and Secure Boot Enforcement](mitigation-library.md#cryptographically-signed-firmware-and-secure-boot-enforcement) (Preventive)
- [Hardened Update and Diagnostic Access Controls](mitigation-library.md#hardened-update-and-diagnostic-access-controls) (Preventive)

### Engine & Powertrain ECU Overload / Destructive DoS

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE: Denial of Service

**Affects:** Engine & powertrain ECU

An attacker who gains access to the powertrain CAN domain (via compromised gateway, telematics, OBD-II, or lateral movement) can flood the Engine Control Unit (ECU) with high-frequency or malformed control messages. By overwhelming the ECU’s processing capacity or suppressing critical sensor data (e.g., temperature, RPM, oil pressure), the attacker can induce incorrect engine behavior. This may disable safety limiters or cause the ECU to miss protective shutdown thresholds, allowing the engine to over-rev, overheat, or run without proper fuel/air balance, leading to catastrophic mechanical failure (“engine blowout”) or permanent damage.

**Attacker goal / impact:** Cause physical damage to the engine (overheating, over-revving) via repeated commands.

**Mitigations**

- [Engine Safety Limiters Enforced at Hardware and ECU Levels](mitigation-library.md#engine-safety-limiters-enforced-at-hardware-and-ecu-levels) (Corrective)
- [Rate-Limited, Authenticated Control Traffic Through a Secure Gateway](mitigation-library.md#rate-limited-authenticated-control-traffic-through-a-secure-gateway) (Preventive)

### Exploiting insecure bootloaders

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE: Tampering

**Affects:** CAN Bus

If ECUs do not enforce secure boot, attackers can load modified or malicious firmware images. This can persist even after power cycles and evade standard diagnostics. Secure boot validation failure is a major vector for long-term compromise.

**Attacker goal / impact:** Bypass trust chain to load malicious OS or firmware on ECUs.

**Mitigations**

- [Locked-Down Bootloader Access and Controlled Update Paths](mitigation-library.md#locked-down-bootloader-access-and-controlled-update-paths) (Preventive)
- [Verified Boot With Hardware-Backed Root of Trust](mitigation-library.md#verified-boot-with-hardware-backed-root-of-trust) (Preventive)

### Memory corruption or buffer overflow in ECU software

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** CWE / STRIDE: Tampering

**Affects:** CAN Bus

Bugs in ECU firmware parsers or network stacks can lead to memory corruption when malformed CAN or diagnostic packets are received. Attackers can exploit these vulnerabilities to execute arbitrary code. This is especially dangerous when firmware runs with high privilege.

**Attacker goal / impact:** Crash an ECU or execute arbitrary code via malformed packets.

**Mitigations**

- [Input Validation and Gateway-Level Sanitization of Network Traffic](mitigation-library.md#input-validation-and-gateway-level-sanitization-of-network-traffic) (Preventive)
- [Memory-Safe Parsing, Bounds Enforcement, and Hardened Firmware Builds](mitigation-library.md#memory-safe-parsing-bounds-enforcement-and-hardened-firmware-builds) (Preventive)

### Replay attacks on CAN traffic

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** STRIDE: Spoofing

**Affects:** CAN Bus

Captured legitimate messages can be replayed at a later time to trigger vehicle actions without authorization. For example, replaying a door-unlock or engine-start command. CAN’s stateless design makes it difficult to distinguish old messages from current ones.

**Attacker goal / impact:** Capture and re-send valid commands (e.g., "Unlock Door") to trigger actions without auth.

**Mitigations**

- [Message Freshness Enforcement With Counters, Nonces, or Timestamps](mitigation-library.md#message-freshness-enforcement-with-counters-nonces-or-timestamps) (Preventive)
- [Secure Gateway Filtering With Context and Rate Validation](mitigation-library.md#secure-gateway-filtering-with-context-and-rate-validation) (Preventive)

### Unauthorized CAN message injection

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE: Tampering

**Affects:** CAN Bus

Attackers can inject forged messages onto the CAN bus to impersonate legitimate ECUs. Since the CAN protocol lacks authentication, other modules may accept and act on malicious commands. This can directly manipulate vehicle behavior, such as disabling brakes or spoofing sensor data.

**Attacker goal / impact:** Send fabricated messages to control steering, acceleration, or braking.

**Mitigations**

- [Secure Gateways With Message Authentication and Signal Validation](mitigation-library.md#secure-gateways-with-message-authentication-and-signal-validation) (Preventive)
- [Segmented CAN Networks With Strict ECU Access Controls](mitigation-library.md#segmented-can-networks-with-strict-ecu-access-controls) (Preventive)

### Key or credential leakage from ECUs

**Priority:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** STRIDE: Info Disclosure

**Affects:** CAN Bus

Some ECUs store cryptographic keys or authentication tokens insecurely in flash or RAM. Physical attackers can extract these through chip-off or debugging interfaces. Once leaked, these secrets allow reprogramming, cloning, or remote unlocking of other vehicles.

**Attacker goal / impact:** Extract cryptographic keys to decrypt firmware or spoof valid messages.

**Mitigations**

- [Hardware-Backed Secure Key Storage and Non-Extractable Secrets](mitigation-library.md#hardware-backed-secure-key-storage-and-non-extractable-secrets) (Preventive)
- [Locked-Down Debug/Programming Interfaces With Secure Access Controls](mitigation-library.md#locked-down-debugprogramming-interfaces-with-secure-access-controls) (Preventive)

## Connectivity & Infotainment (Entry Points)

### Bluetooth exploitation

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** STRIDE: Elevation of Privilege

**Affects:** Bluetooth Controller

Weak Bluetooth implementations or pairing protocols can allow attackers to eavesdrop, inject commands, or access internal data. Exploiting Bluetooth vulnerabilities may not require physical access if the vehicle’s pairing mode is active. Attackers can impersonate trusted devices or trigger DoS conditions.

**Attacker goal / impact:** Remote code execution or pairing without consent to access contacts or unlock the car.

**Mitigations**

- [Hardened Bluetooth Pairing and Authenticated Sessions](mitigation-library.md#hardened-bluetooth-pairing-and-authenticated-sessions) (Preventive)
- [Restricted Bluetooth Attack Surface and Anomaly-Aware Handling](mitigation-library.md#restricted-bluetooth-attack-surface-and-anomaly-aware-handling) (Preventive)

### Compromised mobile app integrations (Android Auto / CarPlay)

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** STRIDE: Spoofing

**Affects:** Infotainment OS

When smartphones connect via Android Auto or Apple CarPlay, vulnerabilities in mobile apps or USB drivers can serve as attack vectors. Malware on the phone could exploit weak isolation between the mobile and infotainment environments. This creates a path for lateral movement into vehicle networks.

**Attacker goal / impact:** Use a compromised phone to send malicious input to the head unit.

**Mitigations**

- [Controlled USB / Wireless Interfaces With Policy Enforcement and Threat Detection](mitigation-library.md#controlled-usb--wireless-interfaces-with-policy-enforcement-and-threat-detection) (Preventive)
- [Strict Isolation and Sandboxing Between Mobile and Infotainment Domains](mitigation-library.md#strict-isolation-and-sandboxing-between-mobile-and-infotainment-domains) (Preventive)

### Security Misconfiguration (Web and Mobile)

**Priority:** High · **Likelihood:** High · **Severity:** High · **Framework:** OWASP: Security Misconfig

**Affects:** Infotainment OS

An attacker could exploit security misconfigurations to gain unauthorized access or functionality. This could include unpatched flaws, unprotected files, and directories, or default accounts.

**Attacker goal / impact:** Default passwords or open debug ports left on the Infotainment OS.

**Mitigations**

- [Harden Assets Against Attacks](mitigation-library.md#harden-assets-against-attacks) (Preventive)
- [Implement a minimal installation](mitigation-library.md#implement-a-minimal-installation) (Preventive)
- [Implement Timely Patching](mitigation-library.md#implement-timely-patching) (Preventive)

### Client-Side Injection

**Priority:** Medium · **Likelihood:** High · **Severity:** Low · **Framework:** OWASP: Injection

**Affects:** Infotainment OS

Attackers exploit vulnerabilities by injecting malicious code (e.g., JavaScript, SQL queries) into the mobile app.

**Attacker goal / impact:** Execute malicious scripts in the Infotainment browser/UI.

**Mitigations**

- [Implement Parameterization](mitigation-library.md#implement-parameterization) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Malicious USB device injection

**Priority:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** STRIDE: Tampering

**Affects:** USB Controller

A malicious USB stick or device can deliver payloads when connected to the media or diagnostic port. These can exploit parsing vulnerabilities in file systems or firmware loaders. Such attacks are particularly dangerous because they often bypass network-based defenses.

**Attacker goal / impact:** Fuzzing the USB stack to crash the Infotainment OS or gain shell access.

**Mitigations**

- [Restricted USB Functionality With Strict Parsing and Allowed Device Profiles](mitigation-library.md#restricted-usb-functionality-with-strict-parsing-and-allowed-device-profiles) (Preventive)
- [USB Port Access Controls and Execution Barriers for Untrusted Devices](mitigation-library.md#usb-port-access-controls-and-execution-barriers-for-untrusted-devices) (Preventive)

### Voice-assistant command injection

**Priority:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** STRIDE: Tampering

**Affects:** Infotainment OS

Voice-recognition interfaces can be tricked by ultrasonic or hidden audio commands (so-called “silent speech attacks”). Attackers may issue commands to dial numbers, access data, or modify system settings. Privacy threats arise when assistants transmit voice data to third-party servers.

**Attacker goal / impact:** Using hidden audio frequencies or recorded voice to trigger commands (e.g., "Open Garage").

**Mitigations**

- [Privacy-Respecting Voice Processing and Restricted Data Exposure](mitigation-library.md#privacy-respecting-voice-processing-and-restricted-data-exposure) (Preventive)
- [User-Verified Actions and Robust Command Authentication](mitigation-library.md#user-verified-actions-and-robust-command-authentication) (Preventive)

### Session Hijacking

**Priority:** Low · **Likelihood:** Medium · **Severity:** Low · **Framework:** OWASP: Broken Access Control

**Affects:** Infotainment OS

An attacker discovers/compromises the session management strategy and gains access to an object by impersonating another user or a service.

**Attacker goal / impact:** Taking over an active user session (e.g., Spotify or Navigation) to steal data.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Secure Service Token Management](mitigation-library.md#secure-service-token-management) (Preventive)

### Side-channel data leakage

**Priority:** Low · **Likelihood:** Low · **Severity:** High · **Framework:** STRIDE: Info Disclosure

**Affects:** Infotainment OS

Sensitive data can be inadvertently exposed through logs, screenshots, or background apps.

**Attacker goal / impact:** Analyzing power consumption or EM emissions to deduce crypto keys (very advanced).

**Mitigations**

- [Audit Logging Configuration](mitigation-library.md#audit-logging-configuration) (Detective)

## Software Lifecycle, Backend & Privacy

### Broken Authentication

**Priority:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** OWASP: Identification Failures

**Affects:** Infotainment OS

Attackers could target authentication mechanisms, potentially gaining complete control of other users' accounts, accessing their data, and performing actions on their behalf.

**Attacker goal / impact:** Weak passwords allowing attackers to log into the vehicle mobile app/account.

**Mitigations**

- [Deploy anti-brute force protections](mitigation-library.md#deploy-anti-brute-force-protections) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Map all authentication flows](mitigation-library.md#map-all-authentication-flows) (Preventive)
- [Secure credential recovery endpoints](mitigation-library.md#secure-credential-recovery-endpoints) (Preventive)

### Exploiting legacy or unsupported firmware

**Priority:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** OWASP: Vulnerable Components

**Affects:** Infotainment System

Vehicles often run outdated infotainment firmware that no longer receives patches. Attackers can use known exploits to compromise such systems indefinitely. These vulnerabilities persist across multiple model years, creating systemic risk.

**Attacker goal / impact:** Attacking known vulnerabilities in old libraries (e.g., old Linux kernel in Infotainment).

**Mitigations**

- [Mandatory Firmware Lifecycle Management and Decommissioning](mitigation-library.md#mandatory-firmware-lifecycle-management-and-decommissioning) (Preventive)
- [Secure Gateway Isolation and Hardening of Legacy Components](mitigation-library.md#secure-gateway-isolation-and-hardening-of-legacy-components) (Preventive)

### Hijacked OTA (Over-the-Air) update mechanisms

**Priority:** Critical · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE: Tampering

**Affects:** Infotainment OS

Compromised OTA servers or unverified firmware packages can inject malicious software into the infotainment unit. Without proper signature verification and secure boot, attackers can install persistent malware. This grants long-term control and surveillance capabilities.

**Attacker goal / impact:** Pushing a malicious firmware update to the entire fleet of vehicles.

**Mitigations**

- [End-to-End Signed OTA Packages With Secure Boot Enforcement](mitigation-library.md#end-to-end-signed-ota-packages-with-secure-boot-enforcement) (Preventive)
- [Hardened OTA Delivery Infrastructure With Authenticated Update Channels](mitigation-library.md#hardened-ota-delivery-infrastructure-with-authenticated-update-channels) (Preventive)

### Insecure Data Storage

**Priority:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** OWASP Mobile: Insecure Storage

**Affects:** Infotainment OS

Sensitive data (like personal information, credentials, or financial data) stored insecurely on the device can be accessed by unauthorized parties if the device is lost, stolen, or compromised.

**Attacker goal / impact:** Storing tokens or keys in plaintext on the Infotainment file system.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)

### Broken access control

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP: Broken Access Control

**Affects:** Infotainment OS

An attacker could exploit broken access control to access unauthorized functionality and data, such as accessing other users' accounts, viewing sensitive files, modifying other users’ data, and changing access rights.

**Attacker goal / impact:** User A accessing User B's vehicle telemetry or location data.

**Mitigations**

- [Deny Access by Default](mitigation-library.md#deny-access-by-default) (Preventive)
- [Develop a comprehensive threat model](mitigation-library.md#develop-a-comprehensive-threat-model) (Preventive)
- [Enforce record ownership in models](mitigation-library.md#enforce-record-ownership-in-models) (Preventive)
- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement access control mechanisms](mitigation-library.md#implement-access-control-mechanisms) (Preventive)

### Cryptographic failure

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** OWASP: Crypto Failures

**Affects:** Infotainment OS

An attacker could exploit cryptographic failures to access sensitive data unprotected, such as credit card information, personal data, or business secrets.

**Attacker goal / impact:** Weak encryption enabling decryption of OTA updates or stored user data.

**Mitigations**

- [Classify data sensitivity](mitigation-library.md#classify-data-sensitivity) (Preventive)
- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)
- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement up-to-date encryption standards](mitigation-library.md#implement-up-to-date-encryption-standards) (Preventive)

### Data Disclosure

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** LINDDUN: Identifiability

**Affects:** Bluetooth Controller, GPS

Excessively collecting, storing, processing, or sharing personal data. The data minimization principle is critical here: only the strictly necessary data should be collected or disclosed. Data disclosure can be explicit, i.e., intended or designed by the system, or implicit, i.e., unintended or indirect (e.g., through metadata or derived from other data). The focus is on four threat characteristics: Unnecessary data types: this relates to the data type sensitivity, granularity, and encoding, which can be too detailed Excessive data volume: this relates to the amount and frequency of the data processing and the number of involved data subjects, which can be too high Unnecessary processing: this relates to the further data treatment analysis, propagation, or retention, which can be considered not strictly necessary Excessive exposure: this relates to the different parties with whom the data is shared, which can be considered too much, and how widely accessible the data is

**Attacker goal / impact:** Leaking GPS history or PII (Personally Identifiable Information) to unauthorized parties.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement an anonymity system](mitigation-library.md#implement-an-anonymity-system) (Preventive)
- [Implement privacy-preserving authentication methods.](mitigation-library.md#implement-privacy-preserving-authentication-methods) (Preventive)
- [Implement privacy-preserving cryptographic protocols](mitigation-library.md#implement-privacy-preserving-cryptographic-protocols) (Preventive)
- [Implement Private Information Retrieval (PIR) techniques.](mitigation-library.md#implement-private-information-retrieval-pir-techniques) (Preventive)
- [Implement pseudonymity systems](mitigation-library.md#implement-pseudonymity-systems) (Preventive)

### Exploiting unpatched software vulnerabilities

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP: Vulnerable Components

**Affects:** Infotainment OS

Attackers may exploit outdated or unpatched software in the infotainment operating system to execute arbitrary code. Once compromised, they can gain control over system functions or pivot to other in-vehicle networks. This often occurs when OEMs delay security updates or use legacy components.

**Attacker goal / impact:** Zero-day attacks on the OS or 3rd party libraries.

**Mitigations**

- [Hardening of Infotainment OS and Isolation From Critical Networks](mitigation-library.md#hardening-of-infotainment-os-and-isolation-from-critical-networks) (Preventive)
- [Regular, Secure, and Verified Software Update Pipelines](mitigation-library.md#regular-secure-and-verified-software-update-pipelines) (Preventive)

### Insecure Inter-Process Communication (IPC)

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** STRIDE: Elevation of Privilege

**Affects:** Infotainment OS

Insecure communication between apps or components can be intercepted or manipulated.

**Attacker goal / impact:** malicious app on Infotainment talking to the Gateway service without permission.

**Mitigations**

- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Insufficient Transport Layer Protection

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP: Crypto Failures

**Affects:** Infotainment OS

Data transmitted between the mobile app and server can be intercepted if not properly encrypted.

**Attacker goal / impact:** Sending telemetry or commands over HTTP instead of HTTPS (Man-in-the-Middle).

**Mitigations**

- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)

### Vulnerable and Outdated Components

**Priority:** High · **Likelihood:** High · **Severity:** High · **Framework:** OWASP: Vulnerable Components

**Affects:** Infotainment OS

An attacker could target vulnerable and outdated components, such as libraries, frameworks, and other software modules, to execute various attacks.

**Attacker goal / impact:** Using libraries with known CVEs (Common Vulnerabilities and Exposures).

**Mitigations**

- [Conduct Software Composition Analysis](mitigation-library.md#conduct-software-composition-analysis) (Detective)
- [Eliminate unused dependencies](mitigation-library.md#eliminate-unused-dependencies) (Preventive)
- [Source trusted libraries and packages](mitigation-library.md#source-trusted-libraries-and-packages) (Preventive)

### Weak Server-Side Controls

**Priority:** High · **Likelihood:** Medium · **Severity:** Critical · **Framework:** OWASP API: Broken Object Level Auth

**Affects:** Infotainment OS

Servers interacting with the mobile app may have vulnerabilities due to improper authentication, authorization, or input validation.

**Attacker goal / impact:** Backend API allowing unverified commands to be sent to the vehicle.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Insecure Communication with Third-Party Services

**Priority:** Medium · **Likelihood:** High · **Severity:** Low · **Framework:** OWASP API: Unsafe Consumption

**Affects:** Infotainment OS

Mobile apps often interact with third-party APIs or services, which may be insecure or malicious.

**Attacker goal / impact:** Intercepting data sent between the car and music/weather services.

**Mitigations**

- [Develop a comprehensive threat model](mitigation-library.md#develop-a-comprehensive-threat-model) (Preventive)
- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)

### Malicious Code and Malware

**Priority:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** STRIDE: Tampering

**Affects:** Infotainment OS

Mobile devices can be infected with malware that can compromise apps, steal data, or perform unauthorized actions.

**Attacker goal / impact:** Ransomware locking the infotainment screen until payment is made.

**Mitigations**

- [Download from trusted sources only](mitigation-library.md#download-from-trusted-sources-only) (Preventive)

### Reverse Engineering

**Priority:** Medium · **Likelihood:** High · **Severity:** Low · **Framework:** STRIDE: Info Disclosure

**Affects:** Infotainment OS

Attackers decompile or reverse-engineer the mobile app to understand its functionality, extract sensitive data, or discover vulnerabilities.

**Attacker goal / impact:** Analyzing app binaries to find API keys or logic flaws.

**Mitigations**

- [Change default credentials immediately](mitigation-library.md#change-default-credentials-immediately) (Preventive)
- [Implement Code Obfuscation](mitigation-library.md#implement-code-obfuscation) (Preventive)
