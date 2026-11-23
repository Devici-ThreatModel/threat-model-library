# Medical Device: Threats

64 curated threats, grouped by theme and ordered by risk. Select a threat for its full description and mitigations. Back to the [model overview](README.md).

## Risk summary

| Risk level | Threats |
|---|---|
| Critical | 12 |
| High | 33 |
| Medium | 14 |
| Low | 2 |
| Unrated | 3 |

## Patient Safety & Device Integrity (Medical Specific)

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Denial-of-therapy or over-therapy due to cyber event](threat-details.md#denial-of-therapy-or-over-therapy-due-to-cyber-event) | Devici Custom Methodology | Medium | Critical | **Critical** | Patient Safety: Stop or overdose therapy (e.g., insulin/pacing). |
| [Improper Memory Buffer Restriction](threat-details.md#improper-memory-buffer-restriction) | CWE | Low | Critical | **High** | Exploit: Buffer overflow leading to code execution. |
| [Insecure boot](threat-details.md#insecure-boot) | CWE | Low | Critical | **High** | Control: Run malicious firmware/rootkit (Lack of Root of Trust). |
| [Insecure firmware update mechanism](threat-details.md#insecure-firmware-update-mechanism) | CWE | Medium | Critical | **High** | Control: Flash malicious OS to device. |
| [Logic flaws in control software that could alter therapy or diagnosis](threat-details.md#logic-flaws-in-control-software-that-could-alter-therapy-or-diagnosis) | Devici Custom Methodology | Medium | Critical | **High** | Patient Safety: Trigger edge-case bugs to alter therapy. |
| [Tampering with calibration data or safety thresholds](threat-details.md#tampering-with-calibration-data-or-safety-thresholds) | Devici Custom Methodology | Low | Critical | **High** | Patient Safety: Disable safety limits or alter sensor readings. |
| [Hidden debug or maintenance interfaces](threat-details.md#hidden-debug-or-maintenance-interfaces) | CWE | Low | High | **Medium** | Access: Bypass auth via exposed hardware ports. |
| [Tampering or firmware extraction](threat-details.md#tampering-or-firmware-extraction) | CWE | Low | High | **Medium** | IP Theft: Extract firmware via JTAG/UART. |

## Mobile Security

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Insecure Data Storage](threat-details.md#insecure-data-storage) | MAESTRO | High | High | **Critical** | Data Theft: Read PHI from unencrypted local files. |
| [M1: Improper Credential Usage](threat-details.md#m1-improper-credential-usage) | MAESTRO | High | High | **Critical** | Account Takeover: Hardcoded/weak tokens in app code. |
| [Malicious Code and Malware](threat-details.md#malicious-code-and-malware) | MAESTRO | High | High | **Critical** | Control: Phone malware captures keystrokes/screen. |
| [App Proxy Attack](threat-details.md#app-proxy-attack) | MAESTRO | High | Medium | **High** | Interception: Inspect/modify traffic via local proxy. |
| [Client-Side Injection](threat-details.md#client-side-injection) | MAESTRO | Medium | High | **High** | Code Exec: Run malicious JS or SQL on the phone. |
| [Insecure Communication with Third-Party Services](threat-details.md#insecure-communication-with-third-party-services) | MAESTRO | High | Medium | **High** | Leakage: Data sent to insecure ad/analytics APIs. |
| [Insecure Inter-Process Communication (IPC)](threat-details.md#insecure-inter-process-communication-ipc) | MAESTRO | Medium | High | **High** | Leakage: Malicious apps read medical app data. |
| [M2: Inadequate Supply Chain Security](threat-details.md#m2-inadequate-supply-chain-security) | MAESTRO | Medium | High | **High** | Backdoor: Compromised SDK/Library in app. |
| [M6: Inadequate Privacy Controls](threat-details.md#m6-inadequate-privacy-controls) | MAESTRO | High | Medium | **High** | Compliance: App over-collects PII or leaks to analytics. |
| [Trojaned or attacker controlled app](threat-details.md#trojaned-or-attacker-controlled-app) | MAESTRO | Medium | High | **High** | Phishing: Fake app mimics the real medical app. |
| [M7: Insufficient Binary Protections](threat-details.md#m7-insufficient-binary-protections) | MAESTRO | High | Medium | **Medium** | Cloning: App is easily decompiled/tampered. |
| [Reverse Engineering](threat-details.md#reverse-engineering) | MAESTRO | High | Medium | **Medium** | IP Theft: Analyze code to find API keys/logic. |
| [Side-channel data leakage](threat-details.md#side-channel-data-leakage) | MAESTRO | High | Low | **Medium** | Leakage: Screenshots or logs leak info to OS. |

## Backend & API Security (OWASP API & Web)

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Broken Object Level Authorization](threat-details.md#broken-object-level-authorization) | OWASP API Security Top 10 | High | High | **Critical** | Data Breach: Access other patients' records (BOLA/IDOR). |
| [Security Misconfiguration (API)](threat-details.md#security-misconfiguration-api) | OWASP API Security Top 10 | High | High | **Critical** | Access: Unpatched flaws or open cloud buckets. |
| [Broken Authentication](threat-details.md#broken-authentication) | OWASP API Security Top 10 | Medium | High | **High** | Account Takeover: Hijack user sessions. |
| [Broken Function Level Authorization](threat-details.md#broken-function-level-authorization) | OWASP API Security Top 10 | Medium | High | **High** | Privilege Esc: User accesses Admin/Clinician APIs. |
| [Unsafe Consumption of APIs](threat-details.md#unsafe-consumption-of-apis) | OWASP API Security Top 10 | Medium | High | **High** | Supply Chain: Integrated 3rd party API is compromised. |
| [Broken Object Property Level Authorization](threat-details.md#broken-object-property-level-authorization) | OWASP API Security Top 10 | Medium | Medium | **Medium** | Data Breach: View hidden sensitive fields (Mass Assignment). |
| [Improper Inventory Management](threat-details.md#improper-inventory-management) | OWASP API Security Top 10 | Medium | Medium | **Medium** | Access: Attackers exploit old/unpatched API versions. |
| [Server Side Request Forgery (SSRF)](threat-details.md#server-side-request-forgery-ssrf) | OWASP API Security Top 10 | Low | High | **Medium** | Network Intrusion: API attacks internal cloud services. |
| [Unrestricted Resource Consumption](threat-details.md#unrestricted-resource-consumption) | OWASP API Security Top 10 | High | Medium | **Medium** | DoS: API exhaustion/crash. |
| [Unrestricted Access to Sensitive Business Flows](threat-details.md#unrestricted-access-to-sensitive-business-flows) | OWASP API Security Top 10 | Low | Low | **Low** | Abuse: Automation of business logic (e.g., spam). |

## Privacy & Compliance (LINDDUN & Regulatory)

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Data Disclosure](threat-details.md#data-disclosure) | LINDDUN | High | High | **Critical** | Privacy Breach: Exposing PII/PHI unnecessarily. |
| [Non-Compliance](threat-details.md#non-compliance) | LINDDUN | High | High | **Critical** | Legal: Violating HIPAA/GDPR/MDR requirements. |
| [Data exfiltration from local storage](threat-details.md#data-exfiltration-from-local-storage) | LINDDUN | Medium | High | **High** | Theft: Copying DB files from device. |
| [Identifying](threat-details.md#identifying) | LINDDUN | High | Medium | **High** | De-anonymization: Learning user identity from data. |
| [Linking](threat-details.md#linking) | LINDDUN | High | Medium | **High** | Re-identification: Correlating data to identify user. |
| [Detecting](threat-details.md#detecting) | LINDDUN | Medium | Medium | **Medium** | Inference: Deducing medical condition by observation. |
| [Unawareness and Unintervenability](threat-details.md#unawareness-and-unintervenability) | LINDDUN | High | Low | **Medium** | Rights Violation: User cannot opt-out or see data. |

## General Cybersecurity

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Broken access control](threat-details.md#broken-access-control) | OWASP Top Ten | High | High | **Critical** | Access: Unauthorized viewing/modifying data. |
| [Credential Leakage](threat-details.md#credential-leakage) | CWE | High | High | **Critical** | Access: Keys/Secrets found in GitHub/Logs. |
| [Security Misconfiguration (Web and Mobile)](threat-details.md#security-misconfiguration-web-and-mobile) | OWASP Top Ten | High | High | **Critical** | Access: Default accounts/unprotected files. |
| [Vulnerable and Outdated Components](threat-details.md#vulnerable-and-outdated-components) | OWASP Top Ten | High | High | **Critical** | Exploit: Using libraries with CVEs (e.g., Log4j). |
| [Bypass Access Control](threat-details.md#bypass-access-control) | OWASP Top Ten | Medium | High | **High** | Access: Force browsing to hidden URLs. |
| [Cryptographic failure](threat-details.md#cryptographic-failure) | CWE | Medium | High | **High** | Exposure: Weak encryption (MD5) or bad keys. |
| [Hard-coded Credentials](threat-details.md#hard-coded-credentials) | CWE | Medium | High | **High** | Access: Backdoor via static password/keys. |
| [Identification and Authentication Failures](threat-details.md#identification-and-authentication-failures) | OWASP Top Ten | Medium | High | **High** | Access: Impersonation of legitimate users. |
| [Information Disclosure](threat-details.md#information-disclosure) | STRIDE | High | Medium | **High** | Leakage: General exposure of system info. |
| [Injection flaws](threat-details.md#injection-flaws) | OWASP Top Ten | Medium | High | **High** | Database Compromise: SQL/Command Injection. |
| [Insufficient Transport Layer Protection](threat-details.md#insufficient-transport-layer-protection) | CWE | Medium | High | **High** | Interception: HTTP instead of HTTPS/TLS. |
| [Least Privilege Principle Violation](threat-details.md#least-privilege-principle-violation) | STRIDE | High | Medium | **High** | Access: Users have too many rights. |
| [Logging Failure](threat-details.md#logging-failure) | CWE | High | Medium | **High** | Blindness: No forensic trail of attacks. |
| [Medical Social Engineering](threat-details.md#medical-social-engineering) | STRIDE | High | Medium | **High** | Access: Tricking clinicians/patients. |
| [Security Logging and Monitoring Failures](threat-details.md#security-logging-and-monitoring-failures) | CWE | High | Medium | **High** | Response: Slow reaction to active breach. |
| [Session Hijacking](threat-details.md#session-hijacking) | OWASP Top Ten | Medium | High | **High** | Account Takeover: Stolen session cookies. |
| [Spoofing](threat-details.md#spoofing) | STRIDE | Medium | High | **High** | Impersonation: Faking device or user identity. |
| [Tampering](threat-details.md#tampering) | STRIDE | Medium | High | **High** | Integrity: Modifying data in transit/at rest. |
| [Weak Server-Side Controls](threat-details.md#weak-server-side-controls) | OWASP Top Ten | High | High | **High** | Bypass: Trusting client input without validation. |
| [Denial of Service](threat-details.md#denial-of-service) | STRIDE | High | Medium | **Medium** | Availability: System offline. |
| [Elevation of Privilege](threat-details.md#elevation-of-privilege) | STRIDE | Low | High | **Medium** | Access: Gaining Root/Admin rights. |
| [Missing authentication](threat-details.md#missing-authentication) | CWE | Low | High | **Medium** | Access: Open endpoints exposed. |
| [Repudiation](threat-details.md#repudiation) | STRIDE | Medium | Low | **Low** | Audit: User denies performing an action. |

## Additional threats

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Physical theft or loss of portable devices (PHI exposure)](threat-details.md#physical-theft-or-loss-of-portable-devices-phi-exposure) |  | n/a | n/a | **Unrated** |  |
| [Time synchronization manipulation (affecting logs, alarms, safety timing)](threat-details.md#time-synchronization-manipulation-affecting-logs-alarms-safety-timing) |  | n/a | n/a | **Unrated** |  |
| [Unauthorized parameter modification (e.g., dose rate, voltage, pacing interval)](threat-details.md#unauthorized-parameter-modification-eg-dose-rate-voltage-pacing-interval) |  | n/a | n/a | **Unrated** |  |
