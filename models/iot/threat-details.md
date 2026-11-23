# IoT Device: Threat Details

For each threat: how the attack works, what it affects, and which mitigations counter it. Mitigation names link to the [mitigation library](mitigation-library.md). Back to the [threat list](threats.md) or the [model overview](README.md).

## Cloud & API Security Threats

### Broken Authentication

**Priority:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** OWASP: Identification Failures

**Affects:** Command Module, Integration APIs, Universal Data aggregator

Attackers could target authentication mechanisms, potentially gaining complete control of other users' accounts, accessing their data, and performing actions on their behalf.

**Attacker goal / impact:** Hijack user sessions to access personal data or control smart home devices remotely.

**Mitigations**

- [Deploy anti-brute force protections](mitigation-library.md#deploy-anti-brute-force-protections) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Map all authentication flows](mitigation-library.md#map-all-authentication-flows) (Preventive)
- [Secure credential recovery endpoints](mitigation-library.md#secure-credential-recovery-endpoints) (Preventive)

### Broken Object Level Authorization

**Priority:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** OWASP API: Broken Object Level Auth

**Affects:** Command Module, Integration APIs, Universal Data aggregator

An attacker could exploit API endpoints with broken object-level authorization by manipulating the object ID in the request, leading to unauthorized access to data.

**Attacker goal / impact:** Manipulate ID parameters (BOLA) to view or control other users' thermostats.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement access control mechanisms](mitigation-library.md#implement-access-control-mechanisms) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)
- [Implement random and unpredictable record IDs](mitigation-library.md#implement-random-and-unpredictable-record-ids) (Preventive)
- [Implement record-level authorization checks for all API endpoints](mitigation-library.md#implement-record-level-authorization-checks-for-all-api-endpoints) (Unspecified)

### Weak, Guessable, or Hardcoded Passwords

**Priority:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** OWASP: Identification Failures

**Affects:** Command Module

Many IoT devices ship with default or hardcoded credentials that attackers can easily discover and reuse across devices. This allows unauthorized access to device management interfaces or APIs, leading to compromise and lateral movement across networks.

**Attacker goal / impact:** Brute-force access to web portals or device SSH interfaces using default credentials.

**Mitigations**

- [Change default credentials immediately](mitigation-library.md#change-default-credentials-immediately) (Preventive)
- [Implement unique first login credentials](mitigation-library.md#implement-unique-first-login-credentials) (Preventive)
- [Secure credential recovery endpoints](mitigation-library.md#secure-credential-recovery-endpoints) (Preventive)

### Account-linking abuse

**Priority:** High · **Likelihood:** Medium · **Severity:** Critical · **Framework:** OWASP API: Broken Authentication

**Affects:** Integration APIs

Compromised Amazon credentials grant HVAC control.

**Attacker goal / impact:** Compromise Amazon/Google credentials to gain remote control of the HVAC system via voice skills.

**Mitigations**

- [Least-Privilege Linking and Server-Side Authorization Checks](mitigation-library.md#least-privilege-linking-and-server-side-authorization-checks) (Preventive)
- [Strong Account Authentication and Protective Controls for Linked Services](mitigation-library.md#strong-account-authentication-and-protective-controls-for-linked-services) (Preventive)

### Broken Function Level Authorization

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP API: Broken Function Level Auth

**Affects:** Command Module, Integration APIs, Universal Data aggregator

An attacker could send legitimate API calls to endpoints they should not have access to, leading to unauthorized access to functionality and potentially service disruption.

**Attacker goal / impact:** Access administrative endpoints (e.g., "force update" or "reset user") as a standard user.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement access control mechanisms](mitigation-library.md#implement-access-control-mechanisms) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)

### Broken Object Property Level Authorization

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP API: Broken Object Property Level Auth

**Affects:** Command Module, Integration APIs, Universal Data aggregator

An attacker could access private/sensitive object properties, potentially leading to data disclosure, corruption, or unauthorized privilege escalation.

**Attacker goal / impact:** Access private fields (e.g., internal Wi-Fi keys, location data) mistakenly exposed in API responses.

**Mitigations**

- [Implement property-level access controls](mitigation-library.md#implement-property-level-access-controls) (Preventive)
- [Implement schema-based response validation](mitigation-library.md#implement-schema-based-response-validation) (Preventive)
- [Limit property exposure](mitigation-library.md#limit-property-exposure) (Preventive)

### Bypass Access Control

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP: Broken Access Control

**Affects:** Command Module, Integration APIs, Universal Data aggregator

As an attacker, I aim to bypass access control checks by modifying the URL via parameter tampering or force browsing, altering the internal application state, manipulating the HTML page, or using specialized attack tools to modify API requests.

**Attacker goal / impact:** Force browsing to hidden URLs to alter device configurations without permission.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Improper Inventory Management

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** OWASP API: Improper Inventory

**Affects:** Command Module, Integration APIs, Universal Data aggregator

Attackers could gain unauthorized access through old API versions, unpatched endpoints, or third parties with weaker security, leading to data leaks or server takeover.

**Attacker goal / impact:** Attack old, unpatched API versions (zombie APIs) that were never decommissioned.

**Mitigations**

- [Automate API documentation generation and restrict access to authorized users only](mitigation-library.md#automate-api-documentation-generation-and-restrict-access-to-authorized-users-only) (Preventive)
- [Catalog integrated services and their data handling](mitigation-library.md#catalog-integrated-services-and-their-data-handling) (Preventive)
- [Document API endpoints](mitigation-library.md#document-api-endpoints) (Preventive)

### Insecure skill-API integration

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP API: Unsafe Consumption

**Affects:** Integration APIs

Weak OAuth or token handling between Alexa and cloud.

**Attacker goal / impact:** Exploit weak OAuth tokens or trust between the Cloud Layer and Voice Assistants.

**Mitigations**

- [Least-Privilege Scopes and Strict Token Validation on APIs](mitigation-library.md#least-privilege-scopes-and-strict-token-validation-on-apis) (Preventive)
- [Standards-Based OAuth Flows With Secure Token Storage and Rotation](mitigation-library.md#standards-based-oauth-flows-with-secure-token-storage-and-rotation) (Preventive)

### Missing authentication

**Priority:** High · **Likelihood:** Low · **Severity:** High · **Framework:** OWASP: Broken Access Control

**Affects:** Command Module, Integration APIs, Universal Data aggregator

The product does not perform any authentication for functionality that requires a provable user identity or consumes a significant amount of resources.

**Attacker goal / impact:** Access critical resource-intensive functions without any identity verification.

**Mitigations**

- [Implement centralized authentication](mitigation-library.md#implement-centralized-authentication) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Security Misconfiguration (API)

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** OWASP: Security Misconfig

**Affects:** Command Module, Integration APIs, Universal Data aggregator

Attackers might exploit unpatched flaws, services with insecure default configurations, or unprotected files and directories, potentially leading to unauthorized access or system compromise.

**Attacker goal / impact:** Exploit default settings, verbose error messages, or unprotected directories to map infrastructure.

**Mitigations**

- [Automate configuration assessments](mitigation-library.md#automate-configuration-assessments) (Detective)
- [Harden Assets Against Attacks](mitigation-library.md#harden-assets-against-attacks) (Preventive)
- [Update configurations regularly](mitigation-library.md#update-configurations-regularly) (Preventive)

### Server Side Request Forgery (SSRF)

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** OWASP: SSRF

**Affects:** Command Module, Integration APIs, Universal Data aggregator

Attackers could exploit SSRF vulnerabilities in APIs to cause internal services enumeration, information disclosure, bypassing firewalls, or server misuse.

**Attacker goal / impact:** Force the Cloud Aggregator to attack internal AWS services (e.g., metadata service) to steal keys.

**Mitigations**

- [Deny Access by Default](mitigation-library.md#deny-access-by-default) (Preventive)
- [Disable HTTP redirections and implement a robust URL parser for client input validation.](mitigation-library.md#disable-http-redirections-and-implement-a-robust-url-parser-for-client-input-validation) (Preventive)
- [Implement network segmentation](mitigation-library.md#implement-network-segmentation) (Preventive)
- [Implement URL Validation with Allowlists](mitigation-library.md#implement-url-validation-with-allowlists) (Preventive)
- [Isolate resource fetching mechanisms within the network.](mitigation-library.md#isolate-resource-fetching-mechanisms-within-the-network) (Preventive)
- [Sanitize Output](mitigation-library.md#sanitize-output) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Unsafe Consumption of APIs

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP API: Unsafe Consumption

**Affects:** Command Module, Integration APIs, Universal Data aggregator

Attackers might identify and compromise other APIs/services integrated with the target API, leading to sensitive information exposure, injections, or denial of service.

**Attacker goal / impact:** Compromise the system via vulnerabilities in third-party weather or mapping APIs.

**Mitigations**

- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)
- [Evaluate service provider API security](mitigation-library.md#evaluate-service-provider-api-security) (Preventive)
- [Validate and sanitize API inputs](mitigation-library.md#validate-and-sanitize-api-inputs) (Preventive)

### Unrestricted Access to Sensitive Business Flows

**Priority:** Medium · **Likelihood:** Medium · **Severity:** Low · **Framework:** OWASP API: Unrestricted Access

**Affects:** Command Module, Integration APIs, Universal Data aggregator

Attackers could exploit sensitive business flows in APIs, causing harm such as preventing legitimate users from purchasing a product or leading to inflation in a game's internal economy.

**Attacker goal / impact:** Automate excessive requests to skew business analytics or deplete cloud credits.

**Mitigations**

- [Block Non-Human Traffic](mitigation-library.md#block-non-human-traffic) (Preventive)
- [Implement CAPTCHA for User Verification](mitigation-library.md#implement-captcha-for-user-verification) (Preventive)
- [Implement device fingerprinting to block unauthorized client devices](mitigation-library.md#implement-device-fingerprinting-to-block-unauthorized-client-devices) (Preventive)

## Device, Firmware & Physical Security Threats

### End-of-life devices

**Priority:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** OWASP: Vulnerable Components

**Affects:** Air Quality & Comfort Device

Unsupported units remain on the network unpatched.

**Attacker goal / impact:** Exploiting unpatched vulnerabilities in legacy devices that are no longer supported.

**Mitigations**

- [Enforced Device Retirement and Network Access Revocation](mitigation-library.md#enforced-device-retirement-and-network-access-revocation) (Preventive)
- [Segmentation and Containment Policies for Legacy Hardware](mitigation-library.md#segmentation-and-containment-policies-for-legacy-hardware) (Preventive)

### Insecure boot chain

**Priority:** Critical · **Likelihood:** Medium · **Severity:** Critical · **Framework:** STRIDE: Tampering

**Affects:** Air Quality & Comfort Device

Lack of secure boot permits modified firmware to load on startup.

**Attacker goal / impact:** Loading malicious OS/firmware at startup to create a persistent botnet node.

**Mitigations**

- [Hardware-Backed Secure Boot With Signature Verification](mitigation-library.md#hardware-backed-secure-boot-with-signature-verification) (Preventive)
- [Protected Bootloaders and Controlled Update Paths](mitigation-library.md#protected-bootloaders-and-controlled-update-paths) (Preventive)

### Insecure provisioning keys

**Priority:** Critical · **Likelihood:** Medium · **Severity:** Critical · **Framework:** OWASP: Cryptographic Failures

**Affects:** Air Quality & Comfort Device

Shared credentials used during device onboarding.

**Attacker goal / impact:** Extracting shared secrets from one device to decrypt traffic for the entire fleet.

**Mitigations**

- [Implement unique first login credentials](mitigation-library.md#implement-unique-first-login-credentials) (Preventive)

### Lack of Secure Update Mechanism

**Priority:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** STRIDE: Tampering

**Affects:** Command Module

Devices that lack cryptographic update validation or fail to receive timely patches remain vulnerable to persistent exploitation. Attackers can inject malicious firmware, downgrade versions, or disrupt functionality through manipulated updates.

**Attacker goal / impact:** Devices remain permanently vulnerable because they cannot be patched OTA.

**Mitigations**

- [Cryptographically Signed Updates With Strict Version and Integrity Validation](mitigation-library.md#cryptographically-signed-updates-with-strict-version-and-integrity-validation) (Preventive)
- [Managed, Timely, and Authenticated Update Delivery](mitigation-library.md#managed-timely-and-authenticated-update-delivery) (Preventive)

### Use of Insecure or Outdated Components

**Priority:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** OWASP: Vulnerable Components

**Affects:** Command Module

IoT products frequently include legacy operating systems, outdated libraries, or unmaintained third-party code. These inherited vulnerabilities provide ready-made entry points for attackers and complicate patching or SBOM management.

**Attacker goal / impact:** Using old Linux kernels or libraries with known CVEs in the device firmware.

**Mitigations**

- [Conduct Software Composition Analysis](mitigation-library.md#conduct-software-composition-analysis) (Detective)
- [Source trusted libraries and packages](mitigation-library.md#source-trusted-libraries-and-packages) (Preventive)
- [Utilize trusted repositories for libraries and dependencies](mitigation-library.md#utilize-trusted-repositories-for-libraries-and-dependencies) (Preventive)

### Compromised manufacturing firmware

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE: Tampering

**Affects:** Air Quality & Comfort Device

Malicious code injected before shipment.

**Attacker goal / impact:** Supply chain attack: Devices arrive with malware pre-installed before reaching the user.

**Mitigations**

- [Post-Manufacturing Attestation and Runtime Integrity Verification](mitigation-library.md#post-manufacturing-attestation-and-runtime-integrity-verification) (Preventive)
- [Secure Manufacturing Pipeline With Signed, Trusted Firmware Images](mitigation-library.md#secure-manufacturing-pipeline-with-signed-trusted-firmware-images) (Preventive)

### Hidden debug interfaces (UART/JTAG)

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** STRIDE: Elevation of Privilege

**Affects:** Air Quality & Comfort Device

Accessible maintenance ports could enable local tampering or firmware extraction.

**Attacker goal / impact:** Physical extraction of firmware, root keys, or Wi-Fi credentials via exposed ports.

**Mitigations**

- [Disable or Lock Down Debug Interfaces in Production Devices](mitigation-library.md#disable-or-lock-down-debug-interfaces-in-production-devices) (Preventive)
- [Physical Hardening and Tamper Detection on Debug Ports](mitigation-library.md#physical-hardening-and-tamper-detection-on-debug-ports) (Preventive (Tamper Resistant))

### Insecure firmware updates

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** OWASP: Cryptographic Failures

**Affects:** Air Quality & Comfort Device

Unsigned or unauthenticated updates allow injection of malicious code or rollback to vulnerable firmware.

**Attacker goal / impact:** Injecting malicious code via unsigned updates or rolling back to vulnerable versions.

**Mitigations**

- [Authenticated Update Channels and Controlled Update Workflow](mitigation-library.md#authenticated-update-channels-and-controlled-update-workflow) (Preventive)
- [Mandatory Signed Updates With Strict Version and Integrity Checks](mitigation-library.md#mandatory-signed-updates-with-strict-version-and-integrity-checks) (Preventive)

### Lack of Device Management

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** OWASP: Security Misconfig

**Affects:** Command Module

Failure to provide secure provisioning, decommissioning, or update mechanisms makes devices difficult to control after deployment. Attackers can exploit unmanaged or orphaned devices to persist on networks or pivot into trusted environments.

**Attacker goal / impact:** Inability to revoke access, wipe data, or decommission lost/stolen devices.

**Mitigations**

- [Centralized Device Management With Mandatory Update and Monitoring Policies](mitigation-library.md#centralized-device-management-with-mandatory-update-and-monitoring-policies) (Preventive)
- [Secure Provisioning, Enrollment, and Lifecycle Controls](mitigation-library.md#secure-provisioning-enrollment-and-lifecycle-controls) (Preventive)

### Counterfeit components

**Priority:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** STRIDE: Tampering

**Affects:** Air Quality & Comfort Device

Non-genuine Wi-Fi or sensor modules with backdoors.

**Attacker goal / impact:** Use of non-genuine Wi-Fi modules containing backdoors or hardware trojans.

**Mitigations**

- [Runtime Integrity Monitoring and Restricted Module Privileges](mitigation-library.md#runtime-integrity-monitoring-and-restricted-module-privileges) (Detective)
- [Trusted Supply Chain With Hardware Attestation and Approved Vendor BOM](mitigation-library.md#trusted-supply-chain-with-hardware-attestation-and-approved-vendor-bom) (Preventive)

### Side-channel or physical tampering

**Priority:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** STRIDE: Tampering

**Affects:** Air Quality & Comfort Device

Attackers with access to the thermostat can probe or replace hardware components.

**Attacker goal / impact:** Analyzing power usage or EM emissions to extract encryption keys.

**Mitigations**

- [Secure Hardware Components With Restricted Interfaces and Non-Extractable Secrets](mitigation-library.md#secure-hardware-components-with-restricted-interfaces-and-non-extractable-secrets) (Preventive)
- [Tamper-Resistant Enclosures and Hardware Integrity Protection](mitigation-library.md#tamper-resistant-enclosures-and-hardware-integrity-protection) (Preventive)

## Operational Logic, Data & Safety Threats

### Elevation of Privilege

**Priority:** Critical · **Likelihood:** Medium · **Severity:** Critical · **Framework:** STRIDE: Elevation of Privilege

**Affects:** Command Module, Amazon S3, Integration APIs, Universal Data aggregator

Elevation of privilege is when an attacker gains unauthorized access to higher-level permissions or rights within a system or application.

**Attacker goal / impact:** Gaining unauthorized administrative rights within the cloud or device OS.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)

### Insecure Data Storage

**Priority:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** OWASP: Cryptographic Failures

**Affects:** Local data store

Sensitive data (like personal information, credentials, or financial data) stored insecurely on the device can be accessed by unauthorized parties if the device is lost, stolen, or compromised.

**Attacker goal / impact:** Storing Wi-Fi passwords or PII in plaintext on local flash memory or S3 buckets.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)

### Denial of Service

**Priority:** High · **Likelihood:** High · **Severity:** High · **Framework:** STRIDE: Denial of Service

**Affects:** Command Module, Amazon S3, Integration APIs, Universal Data aggregator, Local data store

Denial of service (DoS) is an attack that disrupts the normal functioning of a system or network by overwhelming it with excessive traffic or requests.

**Attacker goal / impact:** Flooding the device or cloud to prevent legitimate control (e.g., freezing pipes).

**Mitigations**

- [Implement Distributed Architecture](mitigation-library.md#implement-distributed-architecture) (Preventive (Resilience))

### Information Disclosure

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** STRIDE: Information Disclosure

**Affects:** Command Module, Amazon S3, Integration APIs, Universal Data aggregator, Local data store

Information disclosure is the unintentional exposure or release of confidential or sensitive data to unauthorized individuals or entities.

**Attacker goal / impact:** Leaking sensitive user data or system configurations to unauthorized parties.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Least Privilege Principle Violation

**Priority:** High · **Likelihood:** High · **Severity:** High · **Framework:** STRIDE: Elevation of Privilege

**Affects:** Command Module

An attacker breaches the deny-by-default policy, leading to potential exploitation, data breaches, or unauthorized control over system functionalities.

**Attacker goal / impact:** Services running as root allowing attackers to easily escalate if a service is compromised.

**Mitigations**

- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)

### Logic flaws in control algorithms

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE: Tampering

**Affects:** Command Module

Faults in heating/cooling or purification logic could alter temperature or air-quality regulation, leading to unsafe conditions.

**Attacker goal / impact:** Tricking the system into unsafe states (e.g., running heat and AC simultaneously).

**Mitigations**

- [Formal Verification, Simulation Testing, and Safety-Focused Code Review](mitigation-library.md#formal-verification-simulation-testing-and-safety-focused-code-review) (Preventive)
- [Safety Bounds, Watchdog Monitoring, and Independent Fail-Safe Controllers](mitigation-library.md#safety-bounds-watchdog-monitoring-and-independent-fail-safe-controllers) (Corrective (Safety Fail-Safe))

### Power or battery sabotage

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE: Denial of Service

**Affects:** Air Quality & Comfort Device

Frequent relay cycling shortens hardware life or causes HVAC compressor failure.

**Attacker goal / impact:** Rapidly cycling relays to physically burn out the HVAC compressor (Hardware damage).

**Mitigations**

- [Hardware-Level Safeguards and Fault Detection for Power Systems](mitigation-library.md#hardware-level-safeguards-and-fault-detection-for-power-systems) (Corrective (Hardware Safety))
- [Relay Protection, Rate-Limiting, and Command Authentication](mitigation-library.md#relay-protection-rate-limiting-and-command-authentication) (Preventive)

### Privacy leakage

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** LINDDUN: Identifiability

**Affects:** Integration APIs

Sensitive environmental or occupancy data exposed through Alexa history.

**Attacker goal / impact:** Exposing user occupancy patterns (when they are home/away) via history logs.

**Mitigations**

- [Anonymize data to protect individual privacy](mitigation-library.md#anonymize-data-to-protect-individual-privacy) (Preventive)
- [Implement privacy-preserving cryptographic protocols](mitigation-library.md#implement-privacy-preserving-cryptographic-protocols) (Preventive)

### Spoofing

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** STRIDE: Spoofing

**Affects:** Command Module, Amazon S3, Integration APIs, Universal Data aggregator

Spoofing is where an attacker masquerades as a trusted entity to gain unauthorized access or deceive recipients.

**Attacker goal / impact:** An attacker masquerades as a trusted device (Data Transporter) to inject fake data.

**Mitigations**

- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Tampering

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** STRIDE: Tampering

**Affects:** Command Module, Amazon S3, Integration APIs, Universal Data aggregator, Local data store

Tampering with data involves unauthorized changes to digital information, often with harmful intent, making it unreliable and leading to serious consequences.

**Attacker goal / impact:** Unauthorized modification of configuration files or sensor calibration data.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement hashing for data integrity verification.](mitigation-library.md#implement-hashing-for-data-integrity-verification) (Detective)

### Thermal or air-quality manipulation

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE: Tampering

**Affects:** Command Module

Attack changes temperature or disables purification, affecting occupant health or energy consumption.

**Attacker goal / impact:** Maliciously setting temperature to unsafe levels (health risk for elderly/pets).

**Mitigations**

- [Safety Bounds, Fail-Safe HVAC Modes, and Anomaly Detection](mitigation-library.md#safety-bounds-fail-safe-hvac-modes-and-anomaly-detection) (Corrective (Safety Fail-Safe))
- [Sensor Fusion Validation and Authenticated Control Commands](mitigation-library.md#sensor-fusion-validation-and-authenticated-control-commands) (Preventive)

### Unvalidated sensor data (MEMS sensors)

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** STRIDE: Tampering

**Affects:** Command Module

Malicious or spoofed readings influence automated control loops (false overheat / filter alerts).

**Attacker goal / impact:** Injecting fake "smoke" or "heat" data to trigger false alarms or shut down systems.

**Mitigations**

- [Control-Loop Hardening With Safety Bounds and Fallback States](mitigation-library.md#control-loop-hardening-with-safety-bounds-and-fallback-states) (Corrective (Safety Fail-Safe))
- [Sensor Input Authentication, Filtering, and Cross-Check Validation](mitigation-library.md#sensor-input-authentication-filtering-and-cross-check-validation) (Preventive)

### Logging Failure

**Priority:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** OWASP: Logging Failures

**Affects:** Local data store

An attacker can attack the App Server, and because it does not log at the correct level, the Response team is unaware of the attack.​

**Attacker goal / impact:** Attackers operate undetected because the system fails to record security events.

**Mitigations**

- [Audit Logging Configuration](mitigation-library.md#audit-logging-configuration) (Detective)
- [Implement a Security Information and Event Management (SIEM) solution.](mitigation-library.md#implement-a-security-information-and-event-management-siem-solution) (Detective)
- [Implement Comprehensive Logging](mitigation-library.md#implement-comprehensive-logging) (Detective)

### Sensor desync or time manipulation

**Priority:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** STRIDE: Tampering

**Affects:** Command Module

False readings cause over-heating, over-cooling, or ozone over-generation.

**Attacker goal / impact:** Spoofing NTP time to confuse scheduling or cause certificate expiration errors.

**Mitigations**

- [Safety-Limited Control Logic With Bounds and Fail-Safe Modes](mitigation-library.md#safety-limited-control-logic-with-bounds-and-fail-safe-modes) (Corrective (Safety Fail-Safe))
- [Time-Synchronized Sensor Validation and Cross-Sensor Plausibility Checks](mitigation-library.md#time-synchronized-sensor-validation-and-cross-sensor-plausibility-checks) (Preventive)

### Unrestricted Resource Consumption

**Priority:** Medium · **Likelihood:** Medium · **Severity:** Low · **Framework:** STRIDE: Denial of Service

**Affects:** Command Module, Integration APIs, Universal Data aggregator, Local data store, Amazon Sagemaker (Analytics)

Attackers could exploit unrestricted resource consumption, leading to DoS due to resource starvation or increased operational costs.

**Attacker goal / impact:** Exhausting cloud storage (S3) or API quotas, causing financial loss to the provider.

**Mitigations**

- [Implement API rate limiting](mitigation-library.md#implement-api-rate-limiting) (Preventive)
- [Implement resource limits](mitigation-library.md#implement-resource-limits) (Preventive)
- [Limit parameter and payload sizes](mitigation-library.md#limit-parameter-and-payload-sizes) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Repudiation

**Priority:** Low · **Likelihood:** Medium · **Severity:** Low · **Framework:** STRIDE: Repudiation

**Affects:** Command Module, Amazon S3, Integration APIs, Universal Data aggregator, Local data store

Repudiation is the rejection or denial of a performed action.

**Attacker goal / impact:** User denies performing an action due to lack of audit trails.

**Mitigations**

- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Log Security Events](mitigation-library.md#log-security-events) (Detective)
