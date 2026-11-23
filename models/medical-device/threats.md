# Medical Device: Threats

64 curated threats, grouped by theme and ordered by priority. For full descriptions and mitigation guidance, download [medical-device-reference.xlsx](medical-device-reference.xlsx). Back to the [model overview](README.md).

## Priority summary

| Priority level | Threats |
|---|---|
| Critical | 12 |
| High | 33 |
| Medium | 14 |
| Low | 2 |
| Unrated | 3 |

## Patient Safety & Device Integrity (Medical Specific)

| Threat | Framework | Likelihood | Severity | Priority | Affects | Attacker goal / impact | Recommended mitigations |
|---|---|---|---|---|---|---|---|
| **Denial-of-therapy or over-therapy due to cyber event** | Devici Custom Methodology | Medium | Critical | **Critical** | Health Controller | Patient Safety: Stop or overdose therapy (e.g., insulin/pacing). | Integrity-Protected Control Commands and Real-Time Anomaly Detection<br>Redundant Safety Controllers and Independent Therapy Safeguards |
| **Improper Memory Buffer Restriction** | CWE | Low | Critical | **High** | Operating System | Exploit: Buffer overflow leading to code execution. | Adopt a memory-safe programming language<br>Enable Data Execution Protection (DEP)<br>Implement ASLR in your software<br>Implement automatic buffer overflow detection mechanisms<br>Implement input validation libraries |
| **Insecure boot** | CWE | Low | Critical | **High** | Operating System | Control: Run malicious firmware/rootkit (Lack of Root of Trust). | Hardware-Backed Secure Boot With Verified Boot Sequence<br>Protected Bootloader Interfaces and Controlled Firmware Update Paths |
| **Insecure firmware update mechanism** | CWE | Medium | Critical | **High** | Operating System | Control: Flash malicious OS to device. | Authorized Update Channels and Controlled Update Workflow<br>Signed and Authenticated Firmware Updates With Strict Integrity Validation |
| **Logic flaws in control software that could alter therapy or diagnosis** | Devici Custom Methodology | Medium | Critical | **High** | Medical App | Patient Safety: Trigger edge-case bugs to alter therapy. | Formal Verification, Simulation Testing, and Safety-Critical Code Review<br>Safety Bounds, Redundant Monitoring, and Independent Fail-Safe Controllers |
| **Tampering with calibration data or safety thresholds** | Devici Custom Methodology | Low | Critical | **High** | Health Controller | Patient Safety: Disable safety limits or alter sensor readings. | Authenticated Calibration Updates With Integrity and Access Controls<br>Immutable Safety Bounds, Redundant Validation, and Tamper Detection |
| **Hidden debug or maintenance interfaces** | CWE | Low | High | **Medium** | Operating System | Access: Bypass auth via exposed hardware ports. | Disable or Cryptographically Lock Debug Interfaces in Production Devices<br>Physical Hardening and Tamper Detection for Service Ports |
| **Tampering or firmware extraction** | CWE | Low | High | **Medium** | Operating System | IP Theft: Extract firmware via JTAG/UART. | Secure Firmware Storage With Hardware-Backed Access Controls<br>Signed Firmware, Integrity Monitoring, and Tamper-Response Mechanisms |

## Mobile Security

| Threat | Framework | Likelihood | Severity | Priority | Affects | Attacker goal / impact | Recommended mitigations |
|---|---|---|---|---|---|---|---|
| **Insecure Data Storage** | MAESTRO | High | High | **Critical** | Other Apps, Updated Medical App, Medical App | Data Theft: Read PHI from unencrypted local files. | Encrypt all sensitive data in transit and at rest |
| **M1: Improper Credential Usage** | MAESTRO | High | High | **Critical** | Medical App | Account Takeover: Hardcoded/weak tokens in app code. | Secure Credential Storage and Elimination of Hardcoded Secrets<br>Strong Credential Lifecycle, Rotation, and Least-Privilege Token Design |
| **Malicious Code and Malware** | MAESTRO | High | High | **Critical** | Other Apps, Updated Medical App, Medical App | Control: Phone malware captures keystrokes/screen. | Download from trusted sources only |
| **App Proxy Attack** | MAESTRO | High | Medium | **High** | Other Apps | Interception: Inspect/modify traffic via local proxy. | Server-Side Command Validation and Device/Session Binding<br>Strict App-to-App Isolation With Authenticated IPC and Scoped Permissions |
| **Client-Side Injection** | MAESTRO | Medium | High | **High** | Other Apps, Updated Medical App, Medical App | Code Exec: Run malicious JS or SQL on the phone. | Implement Parameterization<br>Validate User Input |
| **Insecure Communication with Third-Party Services** | MAESTRO | High | Medium | **High** | Other Apps, Updated Medical App, Medical App | Leakage: Data sent to insecure ad/analytics APIs. | Develop a comprehensive threat model<br>Encrypt all data in transit using secure protocols. |
| **Insecure Inter-Process Communication (IPC)** | MAESTRO | Medium | High | **High** | Other Apps, Updated Medical App, Medical App | Leakage: Malicious apps read medical app data. | Authenticated, Authorized, and Encrypted IPC Channels<br>Validate User Input |
| **M2: Inadequate Supply Chain Security** | MAESTRO | Medium | High | **High** | Medical App | Backdoor: Compromised SDK/Library in app. | Conduct Software Composition Analysis<br>Eliminate unused dependencies<br>Implement multi-party verification in the deployment pipeline<br>Restrict production pipeline access without approval<br>Utilize trusted repositories for libraries and dependencies |
| **M6: Inadequate Privacy Controls** | MAESTRO | High | Medium | **High** | Medical App | Compliance: App over-collects PII or leaks to analytics. | Data Minimization, Consent Enforcement, and Secure Handling of Personal Information<br>Privacy-by-Design Policies With Access Controls and Regulatory Compliance Checks |
| **Trojaned or attacker controlled app** | MAESTRO | Medium | High | **High** | Updated Medical App | Phishing: Fake app mimics the real medical app. | Server-Side Authorization and Strict Command Validation<br>Signed Releases, Verified App Integrity, and Store-Only Distribution |
| **M7: Insufficient Binary Protections** | MAESTRO | High | Medium | **Medium** | Medical App | Cloning: App is easily decompiled/tampered. | Code Obfuscation and Anti-Reverse Engineering Hardening<br>Runtime Integrity, Anti-Debugging, and Tamper Detection |
| **Reverse Engineering** | MAESTRO | High | Medium | **Medium** | Other Apps, Updated Medical App, Medical App | IP Theft: Analyze code to find API keys/logic. | Change default credentials immediately<br>Implement Code Obfuscation |
| **Side-channel data leakage** | MAESTRO | High | Low | **Medium** | Other Apps, Updated Medical App, Medical App | Leakage: Screenshots or logs leak info to OS. | Audit Logging Configuration |

## Backend & API Security (OWASP API & Web)

| Threat | Framework | Likelihood | Severity | Priority | Affects | Attacker goal / impact | Recommended mitigations |
|---|---|---|---|---|---|---|---|
| **Broken Object Level Authorization** | OWASP API Security Top 10 | High | High | **Critical** | Patient Facing Services, Clinician Services | Data Breach: Access other patients' records (BOLA/IDOR). | Implement Access Control Measures<br>Implement access control mechanisms<br>Implement Attribute-Based Access Control (ABAC)<br>Implement random and unpredictable record IDs<br>Implement record-level authorization checks for all API endpoints |
| **Security Misconfiguration (API)** | OWASP API Security Top 10 | High | High | **Critical** | Patient Facing Services, Clinician Services | Access: Unpatched flaws or open cloud buckets. | Automate configuration assessments<br>Harden Assets Against Attacks<br>Update configurations regularly |
| **Broken Authentication** | OWASP API Security Top 10 | Medium | High | **High** | Other Apps, Patient Facing Services, Updated Medical App, Medical App, Clinician Services, Gateway | Account Takeover: Hijack user sessions. | Deploy anti-brute force protections<br>Implement strong authentication with 2FA or MFA.<br>Map all authentication flows<br>Secure credential recovery endpoints |
| **Broken Function Level Authorization** | OWASP API Security Top 10 | Medium | High | **High** | Patient Facing Services, Clinician Services | Privilege Esc: User accesses Admin/Clinician APIs. | Implement Access Control Measures<br>Implement access control mechanisms<br>Implement Attribute-Based Access Control (ABAC) |
| **Unsafe Consumption of APIs** | OWASP API Security Top 10 | Medium | High | **High** | Patient Facing Services, Clinician Services | Supply Chain: Integrated 3rd party API is compromised. | Encrypt all data in transit using secure protocols.<br>Evaluate service provider API security<br>Validate and sanitize API inputs |
| **Broken Object Property Level Authorization** | OWASP API Security Top 10 | Medium | Medium | **Medium** | Patient Facing Services, Clinician Services | Data Breach: View hidden sensitive fields (Mass Assignment). | Implement property-level access controls<br>Implement schema-based response validation<br>Limit property exposure |
| **Improper Inventory Management** | OWASP API Security Top 10 | Medium | Medium | **Medium** | Patient Facing Services, Clinician Services | Access: Attackers exploit old/unpatched API versions. | Automate API documentation generation and restrict access to authorized users only<br>Catalog integrated services and their data handling<br>Document API endpoints |
| **Server Side Request Forgery (SSRF)** | OWASP API Security Top 10 | Low | High | **Medium** | Patient Facing Services, Clinician Services | Network Intrusion: API attacks internal cloud services. | Deny Access by Default<br>Disable HTTP redirections and implement a robust URL parser for client input validation.<br>Implement network segmentation<br>Implement URL Validation with Allowlists<br>Isolate resource fetching mechanisms within the network.<br>Sanitize Output<br>Validate User Input |
| **Unrestricted Resource Consumption** | OWASP API Security Top 10 | High | Medium | **Medium** | Service data, Patient Facing Services, Medical data, Clinician Services, Gateway, Sensor Data | DoS: API exhaustion/crash. | Implement API rate limiting<br>Implement resource limits<br>Limit parameter and payload sizes<br>Validate User Input |
| **Unrestricted Access to Sensitive Business Flows** | OWASP API Security Top 10 | Low | Low | **Low** | Patient Facing Services, Clinician Services | Abuse: Automation of business logic (e.g., spam). | Block Non-Human Traffic<br>Implement CAPTCHA for User Verification<br>Implement device fingerprinting to block unauthorized client devices |

## Privacy & Compliance (LINDDUN & Regulatory)

| Threat | Framework | Likelihood | Severity | Priority | Affects | Attacker goal / impact | Recommended mitigations |
|---|---|---|---|---|---|---|---|
| **Data Disclosure** | LINDDUN | High | High | **Critical** | Operating System | Privacy Breach: Exposing PII/PHI unnecessarily. | Encrypt all sensitive data in transit and at rest<br>Implement Access Control Measures<br>Implement an anonymity system<br>Implement privacy-preserving authentication methods.<br>Implement privacy-preserving cryptographic protocols<br>Implement Private Information Retrieval (PIR) techniques.<br>Implement pseudonymity systems |
| **Non-Compliance** | LINDDUN | High | High | **Critical** | Medical data, Medical App, Operating System | Legal: Violating HIPAA/GDPR/MDR requirements. | Implement policy and feedback tools |
| **Data exfiltration from local storage** | LINDDUN | Medium | High | **High** | Sensor Data | Theft: Copying DB files from device. | Encrypted Local Storage With Hardware-Backed Key Protection<br>Restricted Local Access Surfaces With Secure Interfaces and Continuous Monitoring |
| **Identifying** | LINDDUN | High | Medium | **High** | Patient Facing Services, Medical data, Medical App, Clinician Services, Operating System | De-anonymization: Learning user identity from data. | Anonymize data to protect individual privacy<br>Implement an anonymity system<br>Implement information hiding techniques<br>Implement privacy-preserving authentication methods.<br>Implement privacy-preserving cryptographic protocols<br>Implement Private Information Retrieval (PIR) techniques.<br>Implement pseudonymity systems |
| **Linking** | LINDDUN | High | Medium | **High** | Medical data | Re-identification: Correlating data to identify user. | Anonymize data to protect individual privacy<br>Implement an anonymity system<br>Implement information hiding techniques<br>Implement privacy-preserving authentication methods.<br>Implement privacy-preserving cryptographic protocols<br>Implement Private Information Retrieval (PIR) techniques.<br>Implement pseudonymity systems |
| **Detecting** | LINDDUN | Medium | Medium | **Medium** | Patient Facing Services, Medical data, Medical App, Clinician Services | Inference: Deducing medical condition by observation. | Encrypt all sensitive data in transit and at rest<br>Implement an anonymity system<br>Implement information hiding techniques<br>Implement Private Information Retrieval (PIR) techniques. |
| **Unawareness and Unintervenability** | LINDDUN | High | Low | **Medium** | Medical data, Medical App, Operating System | Rights Violation: User cannot opt-out or see data. | Implement policy and feedback tools |

## General Cybersecurity

| Threat | Framework | Likelihood | Severity | Priority | Affects | Attacker goal / impact | Recommended mitigations |
|---|---|---|---|---|---|---|---|
| **Broken access control** | OWASP Top Ten | High | High | **Critical** | Other Apps, Updated Medical App, Medical App | Access: Unauthorized viewing/modifying data. | Deny Access by Default<br>Develop a comprehensive threat model<br>Enforce record ownership in models<br>Implement Access Control Measures<br>Implement access control mechanisms<br>Implement Attribute-Based Access Control (ABAC) |
| **Credential Leakage** | CWE | High | High | **Critical** | Operating System | Access: Keys/Secrets found in GitHub/Logs. | Implement a secure secret management solution |
| **Security Misconfiguration (Web and Mobile)** | OWASP Top Ten | High | High | **Critical** | Other Apps, Updated Medical App, Medical App, Operating System | Access: Default accounts/unprotected files. | Harden Assets Against Attacks<br>Implement a minimal installation<br>Implement Timely Patching |
| **Vulnerable and Outdated Components** | OWASP Top Ten | High | High | **Critical** | Other Apps, Updated Medical App, Medical App | Exploit: Using libraries with CVEs (e.g., Log4j). | Conduct Software Composition Analysis<br>Eliminate unused dependencies<br>Source trusted libraries and packages |
| **Bypass Access Control** | OWASP Top Ten | Medium | High | **High** | Patient Facing Services, Clinician Services | Access: Force browsing to hidden URLs. | Implement Access Control Measures<br>Implement Attribute-Based Access Control (ABAC)<br>Implement Role-Based Access Control (RBAC)<br>Validate User Input |
| **Cryptographic failure** | CWE | Medium | High | **High** | Other Apps, Updated Medical App, Medical App, Operating System | Exposure: Weak encryption (MD5) or bad keys. | Classify data sensitivity<br>Encrypt all data in transit using secure protocols.<br>Encrypt all sensitive data in transit and at rest<br>Implement up-to-date encryption standards |
| **Hard-coded Credentials** | CWE | Medium | High | **High** | Operating System | Access: Backdoor via static password/keys. | Implement a secure secret management solution<br>Implement unique first login credentials |
| **Identification and Authentication Failures** | OWASP Top Ten | Medium | High | **High** | Operating System | Access: Impersonation of legitimate users. | Change default credentials immediately<br>Enforce strong password policies<br>Implement strong authentication with 2FA or MFA. |
| **Information Disclosure** | STRIDE | High | Medium | **High** | Service data, Other Apps, Patient Facing Services, Medical data, Updated Medical App, Medical App, Clinician Services, Gateway, Sensor Data | Leakage: General exposure of system info. | Encrypt all sensitive data in transit and at rest<br>Use Trusted Frameworks |
| **Injection flaws** | OWASP Top Ten | Medium | High | **High** | Other Apps, Patient Facing Services, Updated Medical App, Medical App, Clinician Services | Database Compromise: SQL/Command Injection. | Implement an ORM<br>Use safe APIs<br>Validate User Input |
| **Insufficient Transport Layer Protection** | CWE | Medium | High | **High** | Other Apps, Updated Medical App, Medical App | Interception: HTTP instead of HTTPS/TLS. | Encrypt all data in transit using secure protocols. |
| **Least Privilege Principle Violation** | STRIDE | High | Medium | **High** | Other Apps, Updated Medical App, Medical App | Access: Users have too many rights. | Implement Attribute-Based Access Control (ABAC) |
| **Logging Failure** | CWE | High | Medium | **High** | Service data, Medical data, Sensor Data | Blindness: No forensic trail of attacks. | Audit Logging Configuration<br>Implement a Security Information and Event Management (SIEM) solution.<br>Implement Comprehensive Logging |
| **Medical Social Engineering** | STRIDE | High | Medium | **High** | Clinician, Patient | Access: Tricking clinicians/patients. | Continuous Security Awareness Training With Medical-Specific Scenarios<br>Security Awareness Training With PHI-Protection and Scenario Drills<br>Strong Identity Verification and Authorized Change Controls<br>Strong Identity Verification and Role-Based Approval Controls |
| **Security Logging and Monitoring Failures** | CWE | High | Medium | **High** | Operating System | Response: Slow reaction to active breach. | Implement a Security Information and Event Management (SIEM) solution.<br>Implement Comprehensive Logging<br>Log Security Events |
| **Session Hijacking** | OWASP Top Ten | Medium | High | **High** | Other Apps, Updated Medical App, Medical App | Account Takeover: Stolen session cookies. | Encrypt all sensitive data in transit and at rest<br>Implement strong authentication with 2FA or MFA.<br>Secure Service Token Management |
| **Spoofing** | STRIDE | Medium | High | **High** | Other Apps, Patient Facing Services, Updated Medical App, Medical App, Clinician Services, Gateway | Impersonation: Faking device or user identity. | Encrypt all data in transit using secure protocols.<br>Implement strong authentication with 2FA or MFA.<br>Use Trusted Frameworks |
| **Tampering** | STRIDE | Medium | High | **High** | Service data, Other Apps, Patient Facing Services, Medical data, Updated Medical App, Medical App, Clinician Services, Gateway, Sensor Data | Integrity: Modifying data in transit/at rest. | Encrypt all sensitive data in transit and at rest<br>Implement hashing for data integrity verification. |
| **Weak Server-Side Controls** | OWASP Top Ten | High | High | **High** | Other Apps, Updated Medical App, Medical App | Bypass: Trusting client input without validation. | Implement Access Control Measures<br>Use Trusted Frameworks<br>Validate User Input |
| **Denial of Service** | STRIDE | High | Medium | **Medium** | Service data, Other Apps, Patient Facing Services, Medical data, Updated Medical App, Medical App, Clinician Services, Gateway, Sensor Data | Availability: System offline. | Implement Distributed Architecture |
| **Elevation of Privilege** | STRIDE | Low | High | **Medium** | Other Apps, Patient Facing Services, Updated Medical App, Medical App, Clinician Services, Gateway | Access: Gaining Root/Admin rights. | Implement Access Control Measures<br>Implement Attribute-Based Access Control (ABAC) |
| **Missing authentication** | CWE | Low | High | **Medium** | Other Apps, Patient Facing Services, Updated Medical App, Medical App, Clinician Services, Gateway | Access: Open endpoints exposed. | Implement centralized authentication<br>Use Trusted Frameworks |
| **Repudiation** | STRIDE | Medium | Low | **Low** | Service data, Other Apps, Patient Facing Services, Medical data, Updated Medical App, Medical App, Clinician Services, Gateway, Sensor Data | Audit: User denies performing an action. | Implement strong authentication with 2FA or MFA.<br>Log Security Events |

## Additional threats

| Threat | Framework | Likelihood | Severity | Priority | Affects | Attacker goal / impact | Recommended mitigations |
|---|---|---|---|---|---|---|---|
| **Physical theft or loss of portable devices (PHI exposure)** |  | n/a | n/a | **Unrated** | Medical Device |  | Full-Disk Encryption and Secure Credential Storage on All Portable Devices<br>Remote Wipe, Device Tracking, and Access Revocation Controls |
| **Time synchronization manipulation (affecting logs, alarms, safety timing)** |  | n/a | n/a | **Unrated** | Health Controller |  | Authenticated, Redundant, and Tamper-Resistant Time Sources<br>Secure Timestamping and Safety-Window Validation in Control Logic |
| **Unauthorized parameter modification (e.g., dose rate, voltage, pacing interval)** |  | n/a | n/a | **Unrated** | Health Controller |  | Safety-Limited Parameter Ranges With Real-Time Validation and Audit Alerts<br>Strong Authentication, Role-Based Authorization, and Signed Parameter Changes |
