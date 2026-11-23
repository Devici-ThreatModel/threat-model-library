# Medical Device: Threat Details

For each threat: how the attack works, what it affects, and which mitigations counter it. Mitigation names link to the [mitigation library](mitigation-library.md). Back to the [threat list](threats.md) or the [model overview](README.md).

## Patient Safety & Device Integrity (Medical Specific)

### Denial-of-therapy or over-therapy due to cyber event

**Risk:** Critical · **Likelihood:** Medium · **Severity:** Critical · **Framework:** Devici Custom Methodology

**Affects:** Health Controller

A cyberattack or system failure causes the medical device to stop, delay, or excessively deliver therapy—such as halting an infusion pump, disabling pacing, or continuously delivering stimulation—resulting in potential patient harm or device damage.

**Attacker goal / impact:** Patient Safety: Stop or overdose therapy (e.g., insulin/pacing).

**Mitigations**

- [Integrity-Protected Control Commands and Real-Time Anomaly Detection](mitigation-library.md#integrity-protected-control-commands-and-real-time-anomaly-detection) (Detective)
- [Redundant Safety Controllers and Independent Therapy Safeguards](mitigation-library.md#redundant-safety-controllers-and-independent-therapy-safeguards) (Preventive)

### Improper Memory Buffer Restriction

**Risk:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** CWE

**Affects:** Operating System

The product performs operations on a memory buffer, but an attacker can read from or write to a memory location outside the buffer's intended boundary.

**Attacker goal / impact:** Exploit: Buffer overflow leading to code execution.

**Mitigations**

- [Adopt a memory-safe programming language](mitigation-library.md#adopt-a-memory-safe-programming-language) (Preventive)
- [Enable Data Execution Protection (DEP)](mitigation-library.md#enable-data-execution-protection-dep) (Preventive)
- [Implement ASLR in your software](mitigation-library.md#implement-aslr-in-your-software) (Preventive)
- [Implement automatic buffer overflow detection mechanisms](mitigation-library.md#implement-automatic-buffer-overflow-detection-mechanisms) (Detective)
- [Implement input validation libraries](mitigation-library.md#implement-input-validation-libraries) (Preventive)

### Insecure boot

**Risk:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** CWE

**Affects:** Operating System

Without a secure boot chain (root of trust → authenticated bootloader → signed firmware → measured OS), the device cannot cryptographically guarantee that only vendor-approved code runs at boot. This enables attackers to replace or modify firmware, implant persistent rootkits in early-boot stages, bypass higher-level software protections, and evade detection by tampering with logging or attestation mechanisms.

**Attacker goal / impact:** Control: Run malicious firmware/rootkit (Lack of Root of Trust).

**Mitigations**

- [Hardware-Backed Secure Boot With Verified Boot Sequence](mitigation-library.md#hardware-backed-secure-boot-with-verified-boot-sequence) (Preventive)
- [Protected Bootloader Interfaces and Controlled Firmware Update Paths](mitigation-library.md#protected-bootloader-interfaces-and-controlled-firmware-update-paths) (Preventive)

### Insecure firmware update mechanism

**Risk:** High · **Likelihood:** Medium · **Severity:** Critical · **Framework:** CWE

**Affects:** Operating System

The device accepts firmware updates without properly verifying authenticity, integrity, or authorization of the update package or the update source.

**Attacker goal / impact:** Control: Flash malicious OS to device.

**Mitigations**

- [Authorized Update Channels and Controlled Update Workflow](mitigation-library.md#authorized-update-channels-and-controlled-update-workflow) (Preventive)
- [Signed and Authenticated Firmware Updates With Strict Integrity Validation](mitigation-library.md#signed-and-authenticated-firmware-updates-with-strict-integrity-validation) (Preventive)

### Logic flaws in control software that could alter therapy or diagnosis

**Risk:** High · **Likelihood:** Medium · **Severity:** Critical · **Framework:** Devici Custom Methodology

**Affects:** Medical App

Defects or design errors in the device’s control logic can cause incorrect operation of therapeutic or diagnostic functions. An attacker or unintended condition could trigger these flaws to alter dosage, measurement, or timing—resulting in inaccurate diagnosis, inappropriate therapy delivery, or patient harm.

**Attacker goal / impact:** Patient Safety: Trigger edge-case bugs to alter therapy.

**Mitigations**

- [Formal Verification, Simulation Testing, and Safety-Critical Code Review](mitigation-library.md#formal-verification-simulation-testing-and-safety-critical-code-review) (Preventive)
- [Safety Bounds, Redundant Monitoring, and Independent Fail-Safe Controllers](mitigation-library.md#safety-bounds-redundant-monitoring-and-independent-fail-safe-controllers) (Preventive)

### Tampering with calibration data or safety thresholds

**Risk:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** Devici Custom Methodology

**Affects:** Health Controller

An attacker or unauthorized user modifies the device’s calibration constants, sensor offsets, or safety thresholds (e.g., pressure limits, temperature bounds, dosage cutoffs), causing inaccurate readings, unsafe therapy delivery, or disabled safety mechanisms.

**Attacker goal / impact:** Patient Safety: Disable safety limits or alter sensor readings.

**Mitigations**

- [Authenticated Calibration Updates With Integrity and Access Controls](mitigation-library.md#authenticated-calibration-updates-with-integrity-and-access-controls) (Preventive)
- [Immutable Safety Bounds, Redundant Validation, and Tamper Detection](mitigation-library.md#immutable-safety-bounds-redundant-validation-and-tamper-detection) (Preventive)

### Hidden debug or maintenance interfaces

**Risk:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** CWE

**Affects:** Operating System

The device includes hardware or software service interfaces (e.g., UART, JTAG, USB serial, or proprietary maintenance modes) intended for manufacturing, calibration, or servicing. If these interfaces remain accessible, undocumented, or insufficiently protected in the production environment, an attacker with physical or insider access could exploit them to gain unauthorized control of the device.

**Attacker goal / impact:** Access: Bypass auth via exposed hardware ports.

**Mitigations**

- [Disable or Cryptographically Lock Debug Interfaces in Production Devices](mitigation-library.md#disable-or-cryptographically-lock-debug-interfaces-in-production-devices) (Preventive)
- [Physical Hardening and Tamper Detection for Service Ports](mitigation-library.md#physical-hardening-and-tamper-detection-for-service-ports) (Preventive)

### Tampering or firmware extraction

**Risk:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** CWE

**Affects:** Operating System

An attacker with physical, local, or privileged logical access extracts or tampers with the device’s firmware (via JTAG, UART, USB, removable storage, or an unauthenticated update channel), enabling reverse-engineering, creation of modified firmware images, or injection of malicious code that alters device behavior, exposes PHI, or creates persistent backdoors.

**Attacker goal / impact:** IP Theft: Extract firmware via JTAG/UART.

**Mitigations**

- [Secure Firmware Storage With Hardware-Backed Access Controls](mitigation-library.md#secure-firmware-storage-with-hardware-backed-access-controls) (Preventive)
- [Signed Firmware, Integrity Monitoring, and Tamper-Response Mechanisms](mitigation-library.md#signed-firmware-integrity-monitoring-and-tamper-response-mechanisms) (Preventive)

## Mobile Security

### Insecure Data Storage

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** MAESTRO

**Affects:** Other Apps, Updated Medical App, Medical App

Sensitive data (like personal information, credentials, or financial data) stored insecurely on the device can be accessed by unauthorized parties if the device is lost, stolen, or compromised.

**Attacker goal / impact:** Data Theft: Read PHI from unencrypted local files.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)

### M1: Improper Credential Usage

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** MAESTRO

**Affects:** Medical App

Apps store or handle credentials insecurely (e.g., plaintext storage, hardcoded secrets, weak tokens). Attackers can extract or reuse credentials to impersonate users or access backend systems.

**Attacker goal / impact:** Account Takeover: Hardcoded/weak tokens in app code.

**Mitigations**

- [Secure Credential Storage and Elimination of Hardcoded Secrets](mitigation-library.md#secure-credential-storage-and-elimination-of-hardcoded-secrets) (Preventive)
- [Strong Credential Lifecycle, Rotation, and Least-Privilege Token Design](mitigation-library.md#strong-credential-lifecycle-rotation-and-least-privilege-token-design) (Preventive)

### Malicious Code and Malware

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** MAESTRO

**Affects:** Other Apps, Updated Medical App, Medical App

Mobile devices can be infected with malware that can compromise apps, steal data, or perform unauthorized actions.

**Attacker goal / impact:** Control: Phone malware captures keystrokes/screen.

**Mitigations**

- [Download from trusted sources only](mitigation-library.md#download-from-trusted-sources-only) (Preventive)

### App Proxy Attack

**Risk:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** MAESTRO

**Affects:** Other Apps

Attacker uses an on phone app to proxy attacks against the medical app.

**Attacker goal / impact:** Interception: Inspect/modify traffic via local proxy.

**Mitigations**

- [Server-Side Command Validation and Device/Session Binding](mitigation-library.md#server-side-command-validation-and-devicesession-binding) (Preventive)
- [Strict App-to-App Isolation With Authenticated IPC and Scoped Permissions](mitigation-library.md#strict-app-to-app-isolation-with-authenticated-ipc-and-scoped-permissions) (Preventive)

### Client-Side Injection

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** MAESTRO

**Affects:** Other Apps, Updated Medical App, Medical App

Attackers exploit vulnerabilities by injecting malicious code (e.g., JavaScript, SQL queries) into the mobile app.

**Attacker goal / impact:** Code Exec: Run malicious JS or SQL on the phone.

**Mitigations**

- [Implement Parameterization](mitigation-library.md#implement-parameterization) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Insecure Communication with Third-Party Services

**Risk:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** MAESTRO

**Affects:** Other Apps, Updated Medical App, Medical App

Mobile apps often interact with third-party APIs or services, which may be insecure or malicious.

**Attacker goal / impact:** Leakage: Data sent to insecure ad/analytics APIs.

**Mitigations**

- [Develop a comprehensive threat model](mitigation-library.md#develop-a-comprehensive-threat-model) (Preventive)
- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)

### Insecure Inter-Process Communication (IPC)

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** MAESTRO

**Affects:** Other Apps, Updated Medical App, Medical App

Insecure communication between apps or components can be intercepted or manipulated.

**Attacker goal / impact:** Leakage: Malicious apps read medical app data.

**Mitigations**

- [Authenticated, Authorized, and Encrypted IPC Channels](mitigation-library.md#authenticated-authorized-and-encrypted-ipc-channels) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### M2: Inadequate Supply Chain Security

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** MAESTRO

**Affects:** Medical App

Third-party SDKs, libraries, or build pipelines are compromised or unverified. Malicious components introduce backdoors or data-leakage paths into otherwise secure mobile apps.

**Attacker goal / impact:** Backdoor: Compromised SDK/Library in app.

**Mitigations**

- [Conduct Software Composition Analysis](mitigation-library.md#conduct-software-composition-analysis) (Detective)
- [Eliminate unused dependencies](mitigation-library.md#eliminate-unused-dependencies) (Preventive)
- [Implement multi-party verification in the deployment pipeline](mitigation-library.md#implement-multi-party-verification-in-the-deployment-pipeline) (Preventive)
- [Restrict production pipeline access without approval](mitigation-library.md#restrict-production-pipeline-access-without-approval) (Preventive)
- [Utilize trusted repositories for libraries and dependencies](mitigation-library.md#utilize-trusted-repositories-for-libraries-and-dependencies) (Preventive)

### M6: Inadequate Privacy Controls

**Risk:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** MAESTRO

**Affects:** Medical App

Apps over-collect, mishandle, or expose personal and health data. Unauthorized analytics or storage leaks can result in privacy violations and regulatory non-compliance (e.g., HIPAA, GDPR).

**Attacker goal / impact:** Compliance: App over-collects PII or leaks to analytics.

**Mitigations**

- [Data Minimization, Consent Enforcement, and Secure Handling of Personal Information](mitigation-library.md#data-minimization-consent-enforcement-and-secure-handling-of-personal-information) (Preventive)
- [Privacy-by-Design Policies With Access Controls and Regulatory Compliance Checks](mitigation-library.md#privacy-by-design-policies-with-access-controls-and-regulatory-compliance-checks) (Preventive)

### Trojaned or attacker controlled app

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** MAESTRO

**Affects:** Updated Medical App

Attacker violates the app store or update channel, loading an attacker controlled software version onto the Patient's cell phone.

**Attacker goal / impact:** Phishing: Fake app mimics the real medical app.

**Mitigations**

- [Server-Side Authorization and Strict Command Validation](mitigation-library.md#server-side-authorization-and-strict-command-validation) (Preventive)
- [Signed Releases, Verified App Integrity, and Store-Only Distribution](mitigation-library.md#signed-releases-verified-app-integrity-and-store-only-distribution) (Preventive)

### M7: Insufficient Binary Protections

**Risk:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** MAESTRO

**Affects:** Medical App

Lack of code obfuscation, anti-debugging, or integrity checks allows reverse engineering. Attackers extract keys, modify app logic, or repackage trojanized versions.

**Attacker goal / impact:** Cloning: App is easily decompiled/tampered.

**Mitigations**

- [Code Obfuscation and Anti-Reverse Engineering Hardening](mitigation-library.md#code-obfuscation-and-anti-reverse-engineering-hardening) (Preventive)
- [Runtime Integrity, Anti-Debugging, and Tamper Detection](mitigation-library.md#runtime-integrity-anti-debugging-and-tamper-detection) (Detective)

### Reverse Engineering

**Risk:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** MAESTRO

**Affects:** Other Apps, Updated Medical App, Medical App

Attackers decompile or reverse-engineer the mobile app to understand its functionality, extract sensitive data, or discover vulnerabilities.

**Attacker goal / impact:** IP Theft: Analyze code to find API keys/logic.

**Mitigations**

- [Change default credentials immediately](mitigation-library.md#change-default-credentials-immediately) (Corrective)
- [Implement Code Obfuscation](mitigation-library.md#implement-code-obfuscation) (Preventive)

### Side-channel data leakage

**Risk:** Medium · **Likelihood:** High · **Severity:** Low · **Framework:** MAESTRO

**Affects:** Other Apps, Updated Medical App, Medical App

Sensitive data can be inadvertently exposed through logs, screenshots, or background apps.

**Attacker goal / impact:** Leakage: Screenshots or logs leak info to OS.

**Mitigations**

- [Audit Logging Configuration](mitigation-library.md#audit-logging-configuration) (Detective)

## Backend & API Security (OWASP API & Web)

### Broken Object Level Authorization

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** OWASP API Security Top 10

**Affects:** Patient Facing Services, Clinician Services

An attacker could exploit API endpoints with broken object-level authorization by manipulating the object ID in the request, leading to unauthorized access to data.

**Attacker goal / impact:** Data Breach: Access other patients' records (BOLA/IDOR).

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement access control mechanisms](mitigation-library.md#implement-access-control-mechanisms) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)
- [Implement random and unpredictable record IDs](mitigation-library.md#implement-random-and-unpredictable-record-ids) (Preventive)
- [Implement record-level authorization checks for all API endpoints](mitigation-library.md#implement-record-level-authorization-checks-for-all-api-endpoints) (Preventive)

### Security Misconfiguration (API)

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** OWASP API Security Top 10

**Affects:** Patient Facing Services, Clinician Services

Attackers might exploit unpatched flaws, services with insecure default configurations, or unprotected files and directories, potentially leading to unauthorized access or system compromise.

**Attacker goal / impact:** Access: Unpatched flaws or open cloud buckets.

**Mitigations**

- [Automate configuration assessments](mitigation-library.md#automate-configuration-assessments) (Detective)
- [Harden Assets Against Attacks](mitigation-library.md#harden-assets-against-attacks) (Preventive)
- [Update configurations regularly](mitigation-library.md#update-configurations-regularly) (Corrective)

### Broken Authentication

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP API Security Top 10

**Affects:** Other Apps, Patient Facing Services, Updated Medical App, Medical App, Clinician Services, Gateway

Attackers could target authentication mechanisms, potentially gaining complete control of other users' accounts, accessing their data, and performing actions on their behalf.

**Attacker goal / impact:** Account Takeover: Hijack user sessions.

**Mitigations**

- [Deploy anti-brute force protections](mitigation-library.md#deploy-anti-brute-force-protections) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Map all authentication flows](mitigation-library.md#map-all-authentication-flows) (Preventive)
- [Secure credential recovery endpoints](mitigation-library.md#secure-credential-recovery-endpoints) (Preventive)

### Broken Function Level Authorization

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP API Security Top 10

**Affects:** Patient Facing Services, Clinician Services

An attacker could send legitimate API calls to endpoints they should not have access to, leading to unauthorized access to functionality and potentially service disruption.

**Attacker goal / impact:** Privilege Esc: User accesses Admin/Clinician APIs.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement access control mechanisms](mitigation-library.md#implement-access-control-mechanisms) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)

### Unsafe Consumption of APIs

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP API Security Top 10

**Affects:** Patient Facing Services, Clinician Services

Attackers might identify and compromise other APIs/services integrated with the target API, leading to sensitive information exposure, injections, or denial of service.

**Attacker goal / impact:** Supply Chain: Integrated 3rd party API is compromised.

**Mitigations**

- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)
- [Evaluate service provider API security](mitigation-library.md#evaluate-service-provider-api-security) (Preventive)
- [Validate and sanitize API inputs](mitigation-library.md#validate-and-sanitize-api-inputs) (Preventive)

### Broken Object Property Level Authorization

**Risk:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** OWASP API Security Top 10

**Affects:** Patient Facing Services, Clinician Services

An attacker could access private/sensitive object properties, potentially leading to data disclosure, corruption, or unauthorized privilege escalation.

**Attacker goal / impact:** Data Breach: View hidden sensitive fields (Mass Assignment).

**Mitigations**

- [Implement property-level access controls](mitigation-library.md#implement-property-level-access-controls) (Preventive)
- [Implement schema-based response validation](mitigation-library.md#implement-schema-based-response-validation) (Preventive)
- [Limit property exposure](mitigation-library.md#limit-property-exposure) (Preventive)

### Improper Inventory Management

**Risk:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** OWASP API Security Top 10

**Affects:** Patient Facing Services, Clinician Services

Attackers could gain unauthorized access through old API versions, unpatched endpoints, or third parties with weaker security, leading to data leaks or server takeover.

**Attacker goal / impact:** Access: Attackers exploit old/unpatched API versions.

**Mitigations**

- [Automate API documentation generation and restrict access to authorized users only](mitigation-library.md#automate-api-documentation-generation-and-restrict-access-to-authorized-users-only) (Preventive)
- [Catalog integrated services and their data handling](mitigation-library.md#catalog-integrated-services-and-their-data-handling) (Preventive)
- [Document API endpoints](mitigation-library.md#document-api-endpoints) (Preventive)

### Server Side Request Forgery (SSRF)

**Risk:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** OWASP API Security Top 10

**Affects:** Patient Facing Services, Clinician Services

Attackers could exploit SSRF vulnerabilities in APIs to cause internal services enumeration, information disclosure, bypassing firewalls, or server misuse.

**Attacker goal / impact:** Network Intrusion: API attacks internal cloud services.

**Mitigations**

- [Deny Access by Default](mitigation-library.md#deny-access-by-default) (Preventive)
- [Disable HTTP redirections and implement a robust URL parser for client input validation.](mitigation-library.md#disable-http-redirections-and-implement-a-robust-url-parser-for-client-input-validation) (Preventive)
- [Implement network segmentation](mitigation-library.md#implement-network-segmentation) (Preventive)
- [Implement URL Validation with Allowlists](mitigation-library.md#implement-url-validation-with-allowlists) (Preventive)
- [Isolate resource fetching mechanisms within the network.](mitigation-library.md#isolate-resource-fetching-mechanisms-within-the-network) (Preventive)
- [Sanitize Output](mitigation-library.md#sanitize-output) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Unrestricted Resource Consumption

**Risk:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** OWASP API Security Top 10

**Affects:** Service data, Patient Facing Services, Medical data, Clinician Services, Gateway, Sensor Data

Attackers could exploit unrestricted resource consumption, leading to DoS due to resource starvation or increased operational costs.

**Attacker goal / impact:** DoS: API exhaustion/crash.

**Mitigations**

- [Implement API rate limiting](mitigation-library.md#implement-api-rate-limiting) (Preventive)
- [Implement resource limits](mitigation-library.md#implement-resource-limits) (Preventive)
- [Limit parameter and payload sizes](mitigation-library.md#limit-parameter-and-payload-sizes) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Unrestricted Access to Sensitive Business Flows

**Risk:** Low · **Likelihood:** Low · **Severity:** Low · **Framework:** OWASP API Security Top 10

**Affects:** Patient Facing Services, Clinician Services

Attackers could exploit sensitive business flows in APIs, causing harm such as preventing legitimate users from purchasing a product or leading to inflation in a game's internal economy.

**Attacker goal / impact:** Abuse: Automation of business logic (e.g., spam).

**Mitigations**

- [Block Non-Human Traffic](mitigation-library.md#block-non-human-traffic) (Preventive)
- [Implement CAPTCHA for User Verification](mitigation-library.md#implement-captcha-for-user-verification) (Preventive)
- [Implement device fingerprinting to block unauthorized client devices](mitigation-library.md#implement-device-fingerprinting-to-block-unauthorized-client-devices) (Preventive)

## Privacy & Compliance (LINDDUN & Regulatory)

### Data Disclosure

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** LINDDUN

**Affects:** Operating System

Excessively collecting, storing, processing, or sharing personal data. The data minimization principle is critical here: only the strictly necessary data should be collected or disclosed. Data disclosure can be explicit, i.e., intended or designed by the system, or implicit, i.e., unintended or indirect (e.g., through metadata or derived from other data). The focus is on four threat characteristics: Unnecessary data types: this relates to the data type sensitivity, granularity, and encoding, which can be too detailed Excessive data volume: this relates to the amount and frequency of the data processing and the number of involved data subjects, which can be too high Unnecessary processing: this relates to the further data treatment analysis, propagation, or retention, which can be considered not strictly necessary Excessive exposure: this relates to the different parties with whom the data is shared, which can be considered too much, and how widely accessible the data is

**Attacker goal / impact:** Privacy Breach: Exposing PII/PHI unnecessarily.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement an anonymity system](mitigation-library.md#implement-an-anonymity-system) (Preventive)
- [Implement privacy-preserving authentication methods.](mitigation-library.md#implement-privacy-preserving-authentication-methods) (Preventive)
- [Implement privacy-preserving cryptographic protocols](mitigation-library.md#implement-privacy-preserving-cryptographic-protocols) (Preventive)
- [Implement Private Information Retrieval (PIR) techniques.](mitigation-library.md#implement-private-information-retrieval-pir-techniques) (Preventive)
- [Implement pseudonymity systems](mitigation-library.md#implement-pseudonymity-systems) (Preventive)

### Non-Compliance

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** LINDDUN

**Affects:** Medical data, Medical App, Operating System

The system deviates from security and data management best practices, standards, and legislation. Focus is on the organizational and operational management context in which a system or service is embedded. Non-compliance main threat characteristics are: The unlawfulness of personal data processing Lacking data lifecycle management: this relates to data minimization, storage limitation, and data subject control principles A lack of proper cybersecurity risk management

**Attacker goal / impact:** Legal: Violating HIPAA/GDPR/MDR requirements.

**Mitigations**

- [Implement policy and feedback tools](mitigation-library.md#implement-policy-and-feedback-tools) (Preventive)

### Data exfiltration from local storage

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** LINDDUN

**Affects:** Sensor Data

Sensitive patient data and device telemetry stored on the device (e.g., logs, cached PHI, configuration files, or database files) can be read and copied by an attacker with local or logical access. An adversary who gains physical access, exploits a local service vulnerability, or abuses exposed interfaces (USB, removable media, debug ports, or unsecured APIs) can extract PHI or intellectual property and transfer it off-device, leading to privacy breaches, regulatory violations, and targeted follow-on attacks.

**Attacker goal / impact:** Theft: Copying DB files from device.

**Mitigations**

- [Encrypted Local Storage With Hardware-Backed Key Protection](mitigation-library.md#encrypted-local-storage-with-hardware-backed-key-protection) (Preventive)
- [Restricted Local Access Surfaces With Secure Interfaces and Continuous Monitoring](mitigation-library.md#restricted-local-access-surfaces-with-secure-interfaces-and-continuous-monitoring) (Detective)

### Identifying

**Risk:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** LINDDUN

**Affects:** Patient Facing Services, Medical data, Medical App, Clinician Services, Operating System

Learning the identity of an individual. Although many systems require the identification of data subjects, identifying threats arise when the identity can be revealed through leaks, deduction, or inference in cases where this is not intentional or desired. Identifying can be done through Identified data when the system explicitly maintains the link to the identity or refers to the identity (e.g., in the metadata). Identifiable data: The identity can be derived indirectly, e.g., from pseudonyms, identity-revealing content, or through a small anonymity set. Identifying threats is also related to linking. (Re-)identification can also result in unawareness and non-compliance issues.

**Attacker goal / impact:** De-anonymization: Learning user identity from data.

**Mitigations**

- [Anonymize data to protect individual privacy](mitigation-library.md#anonymize-data-to-protect-individual-privacy) (Preventive)
- [Implement an anonymity system](mitigation-library.md#implement-an-anonymity-system) (Preventive)
- [Implement information hiding techniques](mitigation-library.md#implement-information-hiding-techniques) (Preventive)
- [Implement privacy-preserving authentication methods.](mitigation-library.md#implement-privacy-preserving-authentication-methods) (Preventive)
- [Implement privacy-preserving cryptographic protocols](mitigation-library.md#implement-privacy-preserving-cryptographic-protocols) (Preventive)
- [Implement Private Information Retrieval (PIR) techniques.](mitigation-library.md#implement-private-information-retrieval-pir-techniques) (Preventive)
- [Implement pseudonymity systems](mitigation-library.md#implement-pseudonymity-systems) (Preventive)

### Linking

**Risk:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** LINDDUN

**Affects:** Medical data

Associating data items or user actions to learn more about an individual or a group. Linking may lead to unwanted privacy implications, even if it does not reveal one's identity. Data items or user actions can be linked through identifiers: a username, IP address, phone model, sensor type, the combination of data items or sets: a browser fingerprint, location trace profiling, derivation, or inference, and group profiling is a form of linking. In that case, data on a group of individuals is combined in a way that may negatively impact privacy, e.g., through extensive profiling, recommendations, etc. Linking can also lead to identifying, detecting, and non-repudiation threats. Data disclosure threats trigger linking: the more data is available, the more likely linking threats occur.

**Attacker goal / impact:** Re-identification: Correlating data to identify user.

**Mitigations**

- [Anonymize data to protect individual privacy](mitigation-library.md#anonymize-data-to-protect-individual-privacy) (Preventive)
- [Implement an anonymity system](mitigation-library.md#implement-an-anonymity-system) (Preventive)
- [Implement information hiding techniques](mitigation-library.md#implement-information-hiding-techniques) (Preventive)
- [Implement privacy-preserving authentication methods.](mitigation-library.md#implement-privacy-preserving-authentication-methods) (Preventive)
- [Implement privacy-preserving cryptographic protocols](mitigation-library.md#implement-privacy-preserving-cryptographic-protocols) (Preventive)
- [Implement Private Information Retrieval (PIR) techniques.](mitigation-library.md#implement-private-information-retrieval-pir-techniques) (Preventive)
- [Implement pseudonymity systems](mitigation-library.md#implement-pseudonymity-systems) (Preventive)

### Detecting

**Risk:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** LINDDUN

**Affects:** Patient Facing Services, Medical data, Medical App, Clinician Services

Deducing the involvement of an individual by observing. Detecting threats does not require being able to read the actual data – merely knowing that the data exists, is sufficient to infer more (sensitive) information. Detecting can be done through observed communications: the communication to a system or service, or between different systems can be observed, observed application side-effects: actions in an application have side-effects that can be observed. E.g., temporary files in the file system, and evoked system responses: the system leaks the existence of certain data through its responses. These threats also relate to linking and identifying, as the deduced info can be used to extract more info on an individual.

**Attacker goal / impact:** Inference: Deducing medical condition by observation.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement an anonymity system](mitigation-library.md#implement-an-anonymity-system) (Preventive)
- [Implement information hiding techniques](mitigation-library.md#implement-information-hiding-techniques) (Preventive)
- [Implement Private Information Retrieval (PIR) techniques.](mitigation-library.md#implement-private-information-retrieval-pir-techniques) (Preventive)

### Unawareness and Unintervenability

**Risk:** Medium · **Likelihood:** High · **Severity:** Low · **Framework:** LINDDUN

**Affects:** Medical data, Medical App, Operating System

Insufficiently informing, involving or empowering individuals in the processing of personal data. This relates to: Lack of transparency: data subjects are unaware of the collection and/or processing of their data or the personal data of others. Lack of feedback: data subjects are insufficiently informed about the privacy impact they may cause to others using the system. Lack of intervenability: data subjects cannot access or manage their data.

**Attacker goal / impact:** Rights Violation: User cannot opt-out or see data.

**Mitigations**

- [Implement policy and feedback tools](mitigation-library.md#implement-policy-and-feedback-tools) (Preventive)

## General Cybersecurity

### Broken access control

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** OWASP Top Ten

**Affects:** Other Apps, Updated Medical App, Medical App

An attacker could exploit broken access control to access unauthorized functionality and data, such as accessing other users' accounts, viewing sensitive files, modifying other users’ data, and changing access rights.

**Attacker goal / impact:** Access: Unauthorized viewing/modifying data.

**Mitigations**

- [Deny Access by Default](mitigation-library.md#deny-access-by-default) (Preventive)
- [Develop a comprehensive threat model](mitigation-library.md#develop-a-comprehensive-threat-model) (Preventive)
- [Enforce record ownership in models](mitigation-library.md#enforce-record-ownership-in-models) (Preventive)
- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement access control mechanisms](mitigation-library.md#implement-access-control-mechanisms) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)

### Credential Leakage

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** CWE

**Affects:** Operating System

Secrets such as API keys, tokens, or credentials could be accidentally exposed in logs or code.

**Attacker goal / impact:** Access: Keys/Secrets found in GitHub/Logs.

**Mitigations**

- [Implement a secure secret management solution](mitigation-library.md#implement-a-secure-secret-management-solution) (Preventive)

### Security Misconfiguration (Web and Mobile)

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** OWASP Top Ten

**Affects:** Other Apps, Updated Medical App, Medical App, Operating System

An attacker could exploit security misconfigurations to gain unauthorized access or functionality. This could include unpatched flaws, unprotected files, and directories, or default accounts.

**Attacker goal / impact:** Access: Default accounts/unprotected files.

**Mitigations**

- [Harden Assets Against Attacks](mitigation-library.md#harden-assets-against-attacks) (Preventive)
- [Implement a minimal installation](mitigation-library.md#implement-a-minimal-installation) (Preventive)
- [Implement Timely Patching](mitigation-library.md#implement-timely-patching) (Corrective)

### Vulnerable and Outdated Components

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** OWASP Top Ten

**Affects:** Other Apps, Updated Medical App, Medical App

An attacker could target vulnerable and outdated components, such as libraries, frameworks, and other software modules, to execute various attacks.

**Attacker goal / impact:** Exploit: Using libraries with CVEs (e.g., Log4j).

**Mitigations**

- [Conduct Software Composition Analysis](mitigation-library.md#conduct-software-composition-analysis) (Detective)
- [Eliminate unused dependencies](mitigation-library.md#eliminate-unused-dependencies) (Preventive)
- [Source trusted libraries and packages](mitigation-library.md#source-trusted-libraries-and-packages) (Preventive)

### Bypass Access Control

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP Top Ten

**Affects:** Patient Facing Services, Clinician Services

As an attacker, I aim to bypass access control checks by modifying the URL via parameter tampering or force browsing, altering the internal application state, manipulating the HTML page, or using specialized attack tools to modify API requests.

**Attacker goal / impact:** Access: Force browsing to hidden URLs.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)
- [Implement Role-Based Access Control (RBAC)](mitigation-library.md#implement-role-based-access-control-rbac) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Cryptographic failure

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** CWE

**Affects:** Other Apps, Updated Medical App, Medical App, Operating System

An attacker could exploit cryptographic failures to access sensitive data unprotected, such as credit card information, personal data, or business secrets.

**Attacker goal / impact:** Exposure: Weak encryption (MD5) or bad keys.

**Mitigations**

- [Classify data sensitivity](mitigation-library.md#classify-data-sensitivity) (Preventive)
- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)
- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement up-to-date encryption standards](mitigation-library.md#implement-up-to-date-encryption-standards) (Preventive)

### Hard-coded Credentials

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** CWE

**Affects:** Operating System

The product contains hard-coded credentials, such as a password or cryptographic key, which it uses for its inbound authentication, outbound communication to external components, or encryption of internal data.

**Attacker goal / impact:** Access: Backdoor via static password/keys.

**Mitigations**

- [Implement a secure secret management solution](mitigation-library.md#implement-a-secure-secret-management-solution) (Preventive)
- [Implement unique first login credentials](mitigation-library.md#implement-unique-first-login-credentials) (Preventive)

### Identification and Authentication Failures

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP Top Ten

**Affects:** Operating System

An attacker could exploit identification and authentication failures to impersonate legitimate users and gain unauthorized system access.

**Attacker goal / impact:** Access: Impersonation of legitimate users.

**Mitigations**

- [Change default credentials immediately](mitigation-library.md#change-default-credentials-immediately) (Corrective)
- [Enforce strong password policies](mitigation-library.md#enforce-strong-password-policies) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)

### Information Disclosure

**Risk:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** STRIDE

**Affects:** Service data, Other Apps, Patient Facing Services, Medical data, Updated Medical App, Medical App, Clinician Services, Gateway, Sensor Data

Information disclosure is the unintentional exposure or release of confidential or sensitive data to unauthorized individuals or entities.

**Attacker goal / impact:** Leakage: General exposure of system info.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Injection flaws

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP Top Ten

**Affects:** Other Apps, Patient Facing Services, Updated Medical App, Medical App, Clinician Services

An attacker could use injection flaws (like SQL, NoSQL, and OS command injection) to send hostile data to an interpreter, leading to data loss, corruption, lack of accountability, or denial of access. With SQL injection, without sufficient removal or quoting of SQL syntax in user-controllable inputs, the generated SQL query can cause those inputs to be interpreted as SQL instead of ordinary user data. This can be used to alter query logic to bypass security checks or to insert additional statements that modify the back-end database, possibly including the execution of system commands. SQL injection has become a common issue with database-driven websites. The flaw is easily detected and easily exploited. As such, any site or product package with even a minimal user base is likely to be subject to an attempted attack of this kind. This flaw depends on the fact that SQL makes no real distinction between the control and data planes.

**Attacker goal / impact:** Database Compromise: SQL/Command Injection.

**Mitigations**

- [Implement an ORM](mitigation-library.md#implement-an-orm) (Preventive)
- [Use safe APIs](mitigation-library.md#use-safe-apis) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Insufficient Transport Layer Protection

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** CWE

**Affects:** Other Apps, Updated Medical App, Medical App

Data transmitted between the mobile app and server can be intercepted if not properly encrypted.

**Attacker goal / impact:** Interception: HTTP instead of HTTPS/TLS.

**Mitigations**

- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)

### Least Privilege Principle Violation

**Risk:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** STRIDE

**Affects:** Other Apps, Updated Medical App, Medical App

An attacker breaches the deny-by-default policy, leading to potential exploitation, data breaches, or unauthorized control over system functionalities.

**Attacker goal / impact:** Access: Users have too many rights.

**Mitigations**

- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)

### Logging Failure

**Risk:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** CWE

**Affects:** Service data, Medical data, Sensor Data

An attacker can attack the App Server, and because it does not log at the correct level, the Response team is unaware of the attack.​

**Attacker goal / impact:** Blindness: No forensic trail of attacks.

**Mitigations**

- [Audit Logging Configuration](mitigation-library.md#audit-logging-configuration) (Detective)
- [Implement a Security Information and Event Management (SIEM) solution.](mitigation-library.md#implement-a-security-information-and-event-management-siem-solution) (Detective)
- [Implement Comprehensive Logging](mitigation-library.md#implement-comprehensive-logging) (Detective)

### Medical Social Engineering

**Risk:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** STRIDE

**Affects:** Clinician, Patient

An adversary uses deception (phishing, vishing, pretexting, or impersonation) targeted at clinicians, patients, or support staff to trick them into revealing credentials, approving unsafe configuration changes, or disclosing PHI.

**Attacker goal / impact:** Access: Tricking clinicians/patients.

**Mitigations**

- [Continuous Security Awareness Training With Medical-Specific Scenarios](mitigation-library.md#continuous-security-awareness-training-with-medical-specific-scenarios) (Preventive)
- [Security Awareness Training With PHI-Protection and Scenario Drills](mitigation-library.md#security-awareness-training-with-phi-protection-and-scenario-drills) (Preventive)
- [Strong Identity Verification and Authorized Change Controls](mitigation-library.md#strong-identity-verification-and-authorized-change-controls) (Preventive)
- [Strong Identity Verification and Role-Based Approval Controls](mitigation-library.md#strong-identity-verification-and-role-based-approval-controls) (Preventive)

### Security Logging and Monitoring Failures

**Risk:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** CWE

**Affects:** Operating System

An attacker could leverage insufficient logging and monitoring to carry out attacks without being detected, hindering security incident identification and response.

**Attacker goal / impact:** Response: Slow reaction to active breach.

**Mitigations**

- [Implement a Security Information and Event Management (SIEM) solution.](mitigation-library.md#implement-a-security-information-and-event-management-siem-solution) (Detective)
- [Implement Comprehensive Logging](mitigation-library.md#implement-comprehensive-logging) (Detective)
- [Log Security Events](mitigation-library.md#log-security-events) (Detective)

### Session Hijacking

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP Top Ten

**Affects:** Other Apps, Updated Medical App, Medical App

An attacker discovers/compromises the session management strategy and gains access to an object by impersonating another user or a service.

**Attacker goal / impact:** Account Takeover: Stolen session cookies.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Secure Service Token Management](mitigation-library.md#secure-service-token-management) (Preventive)

### Spoofing

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** STRIDE

**Affects:** Other Apps, Patient Facing Services, Updated Medical App, Medical App, Clinician Services, Gateway

Spoofing is where an attacker masquerades as a trusted entity to gain unauthorized access or deceive recipients.

**Attacker goal / impact:** Impersonation: Faking device or user identity.

**Mitigations**

- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Tampering

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** STRIDE

**Affects:** Service data, Other Apps, Patient Facing Services, Medical data, Updated Medical App, Medical App, Clinician Services, Gateway, Sensor Data

Tampering with data involves unauthorized changes to digital information, often with harmful intent, making it unreliable and leading to serious consequences.

**Attacker goal / impact:** Integrity: Modifying data in transit/at rest.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement hashing for data integrity verification.](mitigation-library.md#implement-hashing-for-data-integrity-verification) (Preventive)

### Weak Server-Side Controls

**Risk:** High · **Likelihood:** High · **Severity:** High · **Framework:** OWASP Top Ten

**Affects:** Other Apps, Updated Medical App, Medical App

Servers interacting with the mobile app may have vulnerabilities due to improper authentication, authorization, or input validation.

**Attacker goal / impact:** Bypass: Trusting client input without validation.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Denial of Service

**Risk:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** STRIDE

**Affects:** Service data, Other Apps, Patient Facing Services, Medical data, Updated Medical App, Medical App, Clinician Services, Gateway, Sensor Data

Denial of service (DoS) is an attack that disrupts the normal functioning of a system or network by overwhelming it with excessive traffic or requests.

**Attacker goal / impact:** Availability: System offline.

**Mitigations**

- [Implement Distributed Architecture](mitigation-library.md#implement-distributed-architecture) (Preventive)

### Elevation of Privilege

**Risk:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** STRIDE

**Affects:** Other Apps, Patient Facing Services, Updated Medical App, Medical App, Clinician Services, Gateway

Elevation of privilege is when an attacker gains unauthorized access to higher-level permissions or rights within a system or application.

**Attacker goal / impact:** Access: Gaining Root/Admin rights.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)

### Missing authentication

**Risk:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** CWE

**Affects:** Other Apps, Patient Facing Services, Updated Medical App, Medical App, Clinician Services, Gateway

The product does not perform any authentication for functionality that requires a provable user identity or consumes a significant amount of resources.

**Attacker goal / impact:** Access: Open endpoints exposed.

**Mitigations**

- [Implement centralized authentication](mitigation-library.md#implement-centralized-authentication) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Repudiation

**Risk:** Low · **Likelihood:** Medium · **Severity:** Low · **Framework:** STRIDE

**Affects:** Service data, Other Apps, Patient Facing Services, Medical data, Updated Medical App, Medical App, Clinician Services, Gateway, Sensor Data

Repudiation is the rejection or denial of a performed action.

**Attacker goal / impact:** Audit: User denies performing an action.

**Mitigations**

- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Log Security Events](mitigation-library.md#log-security-events) (Detective)

## Additional threats

### Physical theft or loss of portable devices (PHI exposure)

**Risk:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** Medical Device

Portable medical devices—such as tablets, diagnostic readers, or home-use monitors—may store protected health information (PHI) locally. If such a device is lost or stolen without full-disk encryption or remote wipe capability, an unauthorized individual could access patient data, calibration settings, or device credentials.

**Mitigations**

- [Full-Disk Encryption and Secure Credential Storage on All Portable Devices](mitigation-library.md#full-disk-encryption-and-secure-credential-storage-on-all-portable-devices) (Preventive)
- [Remote Wipe, Device Tracking, and Access Revocation Controls](mitigation-library.md#remote-wipe-device-tracking-and-access-revocation-controls) (Corrective)

### Time synchronization manipulation (affecting logs, alarms, safety timing)

**Risk:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** Health Controller

An attacker tampers with the device’s time source (NTP, GPS, internal RTC, or companion app clock) or manipulates time-stamping mechanisms, causing false timestamps for logs/telemetry, delayed or premature alarms and therapy actions, and incorrect sequencing of safety checks.

**Mitigations**

- [Authenticated, Redundant, and Tamper-Resistant Time Sources](mitigation-library.md#authenticated-redundant-and-tamper-resistant-time-sources) (Preventive)
- [Secure Timestamping and Safety-Window Validation in Control Logic](mitigation-library.md#secure-timestamping-and-safety-window-validation-in-control-logic) (Preventive)

### Unauthorized parameter modification (e.g., dose rate, voltage, pacing interval)

**Risk:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** Health Controller

An attacker or unauthorized user modifies therapy or diagnostic parameters—such as infusion dose rate, stimulation voltage, pacing interval, or calibration settings—without proper authentication or authorization, potentially causing harm to patients or degrading device performance.

**Mitigations**

- [Safety-Limited Parameter Ranges With Real-Time Validation and Audit Alerts](mitigation-library.md#safety-limited-parameter-ranges-with-real-time-validation-and-audit-alerts) (Detective)
- [Strong Authentication, Role-Based Authorization, and Signed Parameter Changes](mitigation-library.md#strong-authentication-role-based-authorization-and-signed-parameter-changes) (Preventive)
