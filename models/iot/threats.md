# IoT Device: Threats

41 curated threats, grouped by theme and ordered by priority. Select a threat for its full description and mitigations. Back to the [model overview](README.md).

## Priority summary

| Priority level | Threats |
|---|---|
| Critical | 10 |
| High | 24 |
| Medium | 6 |
| Low | 1 |

## Cloud & API Security Threats

| Threat | Framework | Likelihood | Severity | Priority | Attacker goal / impact |
|---|---|---|---|---|---|
| [Broken Authentication](threat-details.md#broken-authentication) | OWASP: Identification Failures | High | Critical | **Critical** | Hijack user sessions to access personal data or control smart home devices remotely. |
| [Broken Object Level Authorization](threat-details.md#broken-object-level-authorization) | OWASP API: Broken Object Level Auth | High | Critical | **Critical** | Manipulate ID parameters (BOLA) to view or control other users' thermostats. |
| [Weak, Guessable, or Hardcoded Passwords](threat-details.md#weak-guessable-or-hardcoded-passwords) | OWASP: Identification Failures | High | Critical | **Critical** | Brute-force access to web portals or device SSH interfaces using default credentials. |
| [Account-linking abuse](threat-details.md#account-linking-abuse) | OWASP API: Broken Authentication | Medium | Critical | **High** | Compromise Amazon/Google credentials to gain remote control of the HVAC system via voice skills. |
| [Broken Function Level Authorization](threat-details.md#broken-function-level-authorization) | OWASP API: Broken Function Level Auth | Medium | High | **High** | Access administrative endpoints (e.g., "force update" or "reset user") as a standard user. |
| [Broken Object Property Level Authorization](threat-details.md#broken-object-property-level-authorization) | OWASP API: Broken Object Property Level Auth | Medium | High | **High** | Access private fields (e.g., internal Wi-Fi keys, location data) mistakenly exposed in API responses. |
| [Bypass Access Control](threat-details.md#bypass-access-control) | OWASP: Broken Access Control | Medium | High | **High** | Force browsing to hidden URLs to alter device configurations without permission. |
| [Improper Inventory Management](threat-details.md#improper-inventory-management) | OWASP API: Improper Inventory | High | Medium | **High** | Attack old, unpatched API versions (zombie APIs) that were never decommissioned. |
| [Insecure skill-API integration](threat-details.md#insecure-skill-api-integration) | OWASP API: Unsafe Consumption | Medium | High | **High** | Exploit weak OAuth tokens or trust between the Cloud Layer and Voice Assistants. |
| [Missing authentication](threat-details.md#missing-authentication) | OWASP: Broken Access Control | Low | High | **High** | Access critical resource-intensive functions without any identity verification. |
| [Security Misconfiguration (API)](threat-details.md#security-misconfiguration-api) | OWASP: Security Misconfig | High | Medium | **High** | Exploit default settings, verbose error messages, or unprotected directories to map infrastructure. |
| [Server Side Request Forgery (SSRF)](threat-details.md#server-side-request-forgery-ssrf) | OWASP: SSRF | Low | Critical | **High** | Force the Cloud Aggregator to attack internal AWS services (e.g., metadata service) to steal keys. |
| [Unsafe Consumption of APIs](threat-details.md#unsafe-consumption-of-apis) | OWASP API: Unsafe Consumption | Medium | High | **High** | Compromise the system via vulnerabilities in third-party weather or mapping APIs. |
| [Unrestricted Access to Sensitive Business Flows](threat-details.md#unrestricted-access-to-sensitive-business-flows) | OWASP API: Unrestricted Access | Medium | Low | **Medium** | Automate excessive requests to skew business analytics or deplete cloud credits. |

## Device, Firmware & Physical Security Threats

| Threat | Framework | Likelihood | Severity | Priority | Attacker goal / impact |
|---|---|---|---|---|---|
| [End-of-life devices](threat-details.md#end-of-life-devices) | OWASP: Vulnerable Components | High | High | **Critical** | Exploiting unpatched vulnerabilities in legacy devices that are no longer supported. |
| [Insecure boot chain](threat-details.md#insecure-boot-chain) | STRIDE: Tampering | Medium | Critical | **Critical** | Loading malicious OS/firmware at startup to create a persistent botnet node. |
| [Insecure provisioning keys](threat-details.md#insecure-provisioning-keys) | OWASP: Cryptographic Failures | Medium | Critical | **Critical** | Extracting shared secrets from one device to decrypt traffic for the entire fleet. |
| [Lack of Secure Update Mechanism](threat-details.md#lack-of-secure-update-mechanism) | STRIDE: Tampering | High | Critical | **Critical** | Devices remain permanently vulnerable because they cannot be patched OTA. |
| [Use of Insecure or Outdated Components](threat-details.md#use-of-insecure-or-outdated-components) | OWASP: Vulnerable Components | High | High | **Critical** | Using old Linux kernels or libraries with known CVEs in the device firmware. |
| [Compromised manufacturing firmware](threat-details.md#compromised-manufacturing-firmware) | STRIDE: Tampering | Low | Critical | **High** | Supply chain attack: Devices arrive with malware pre-installed before reaching the user. |
| [Hidden debug interfaces (UART/JTAG)](threat-details.md#hidden-debug-interfaces-uartjtag) | STRIDE: Elevation of Privilege | Medium | High | **High** | Physical extraction of firmware, root keys, or Wi-Fi credentials via exposed ports. |
| [Insecure firmware updates](threat-details.md#insecure-firmware-updates) | OWASP: Cryptographic Failures | Low | Critical | **High** | Injecting malicious code via unsigned updates or rolling back to vulnerable versions. |
| [Lack of Device Management](threat-details.md#lack-of-device-management) | OWASP: Security Misconfig | High | Medium | **High** | Inability to revoke access, wipe data, or decommission lost/stolen devices. |
| [Counterfeit components](threat-details.md#counterfeit-components) | STRIDE: Tampering | Low | High | **Medium** | Use of non-genuine Wi-Fi modules containing backdoors or hardware trojans. |
| [Side-channel or physical tampering](threat-details.md#side-channel-or-physical-tampering) | STRIDE: Tampering | Low | High | **Medium** | Analyzing power usage or EM emissions to extract encryption keys. |

## Operational Logic, Data & Safety Threats

| Threat | Framework | Likelihood | Severity | Priority | Attacker goal / impact |
|---|---|---|---|---|---|
| [Elevation of Privilege](threat-details.md#elevation-of-privilege) | STRIDE: Elevation of Privilege | Medium | Critical | **Critical** | Gaining unauthorized administrative rights within the cloud or device OS. |
| [Insecure Data Storage](threat-details.md#insecure-data-storage) | OWASP: Cryptographic Failures | High | High | **Critical** | Storing Wi-Fi passwords or PII in plaintext on local flash memory or S3 buckets. |
| [Denial of Service](threat-details.md#denial-of-service) | STRIDE: Denial of Service | High | High | **High** | Flooding the device or cloud to prevent legitimate control (e.g., freezing pipes). |
| [Information Disclosure](threat-details.md#information-disclosure) | STRIDE: Information Disclosure | High | Medium | **High** | Leaking sensitive user data or system configurations to unauthorized parties. |
| [Least Privilege Principle Violation](threat-details.md#least-privilege-principle-violation) | STRIDE: Elevation of Privilege | High | High | **High** | Services running as root allowing attackers to easily escalate if a service is compromised. |
| [Logic flaws in control algorithms](threat-details.md#logic-flaws-in-control-algorithms) | STRIDE: Tampering | Low | Critical | **High** | Tricking the system into unsafe states (e.g., running heat and AC simultaneously). |
| [Power or battery sabotage](threat-details.md#power-or-battery-sabotage) | STRIDE: Denial of Service | Low | Critical | **High** | Rapidly cycling relays to physically burn out the HVAC compressor (Hardware damage). |
| [Privacy leakage](threat-details.md#privacy-leakage) | LINDDUN: Identifiability | High | Medium | **High** | Exposing user occupancy patterns (when they are home/away) via history logs. |
| [Spoofing](threat-details.md#spoofing) | STRIDE: Spoofing | Medium | High | **High** | An attacker masquerades as a trusted device (Data Transporter) to inject fake data. |
| [Tampering](threat-details.md#tampering) | STRIDE: Tampering | Medium | High | **High** | Unauthorized modification of configuration files or sensor calibration data. |
| [Thermal or air-quality manipulation](threat-details.md#thermal-or-air-quality-manipulation) | STRIDE: Tampering | Low | Critical | **High** | Maliciously setting temperature to unsafe levels (health risk for elderly/pets). |
| [Unvalidated sensor data (MEMS sensors)](threat-details.md#unvalidated-sensor-data-mems-sensors) | STRIDE: Tampering | Medium | High | **High** | Injecting fake "smoke" or "heat" data to trigger false alarms or shut down systems. |
| [Logging Failure](threat-details.md#logging-failure) | OWASP: Logging Failures | High | Medium | **Medium** | Attackers operate undetected because the system fails to record security events. |
| [Sensor desync or time manipulation](threat-details.md#sensor-desync-or-time-manipulation) | STRIDE: Tampering | Medium | Medium | **Medium** | Spoofing NTP time to confuse scheduling or cause certificate expiration errors. |
| [Unrestricted Resource Consumption](threat-details.md#unrestricted-resource-consumption) | STRIDE: Denial of Service | Medium | Low | **Medium** | Exhausting cloud storage (S3) or API quotas, causing financial loss to the provider. |
| [Repudiation](threat-details.md#repudiation) | STRIDE: Repudiation | Medium | Low | **Low** | User denies performing an action due to lack of audit trails. |
