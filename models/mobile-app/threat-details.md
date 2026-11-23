# Mobile App: Threat Details

For each threat: how the attack works, what it affects, and which mitigations counter it. Mitigation names link to the [mitigation library](mitigation-library.md). Back to the [threat list](threats.md) or the [model overview](README.md).

## All threats

### Broken Authentication

**Risk:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** Spoofing

**Affects:** Application Logic, Local Authentication

Attackers could target authentication mechanisms, potentially gaining complete control of other users' accounts, accessing their data, and performing actions on their behalf.

**Attacker goal / impact:** Account Takeover (ATO); impersonate legitimate users.

**Mitigations**

- [Deploy anti-brute force protections](mitigation-library.md#deploy-anti-brute-force-protections) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Map all authentication flows](mitigation-library.md#map-all-authentication-flows) (Preventive)
- [Secure credential recovery endpoints](mitigation-library.md#secure-credential-recovery-endpoints) (Preventive)

### Credential Theft

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** Spoofing

**Affects:** Local Authentication

An attacker steals or guesses a password using a Brute-force attack, phishing, or credential stuffing provides the password to an AuthC that supports username/password as a fallback authentication mechanism.

**Attacker goal / impact:** Gain valid user credentials via Phishing/Brute-force.

**Mitigations**

- [Eliminate one-factor authentication fallback mechanisms.](mitigation-library.md#eliminate-one-factor-authentication-fallback-mechanisms) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)

### Information Disclosure

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** Information Disclosure

**Affects:** User Interface, Application Logic

Information disclosure is the unintentional exposure or release of confidential or sensitive data to unauthorized individuals or entities.

**Attacker goal / impact:** Leak PII/PHI to unauthorized parties via logs, storage, or net.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Insecure Data Storage

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** Information Disclosure

**Affects:** Application Logic

Sensitive data (like personal information, credentials, or financial data) stored insecurely on the device can be accessed by unauthorized parties if the device is lost, stolen, or compromised.

**Attacker goal / impact:** Read sensitive files from the file system (e.g., if device is lost).

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)

### M1: Improper Credential Usage

**Risk:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** Information Disclosure

**Affects:** Application Logic

Hardcoded credentials, insecure storage or handling of user credentials or API keys, weak credential practices.

**Attacker goal / impact:** Hardcoded keys or weak token storage leading to full breach.

**Mitigations**

- [Secure Credential Storage and Removal of Hardcoded Secrets](mitigation-library.md#secure-credential-storage-and-removal-of-hardcoded-secrets) (Preventive)
- [Strong Credential Handling, Rotation, and Least-Privilege Access](mitigation-library.md#strong-credential-handling-rotation-and-least-privilege-access) (Preventive)

### M3: Insecure Authentication / Authorization

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** Spoofing

**Affects:** Application Logic

Flaws in login flows, token handling, session management, role enforcement, or elevation of privilege.

**Attacker goal / impact:** Flaws in logic allow bypassing auth or assuming roles.

**Mitigations**

- [Robust, Standards-Based Authentication and Secure Session Handling](mitigation-library.md#robust-standards-based-authentication-and-secure-session-handling) (Preventive)
- [Strict Authorization Enforcement with Server-Side Access Controls](mitigation-library.md#strict-authorization-enforcement-with-server-side-access-controls) (Preventive)

### M9: Insecure Data Storage

**Risk:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** Information Disclosure

**Affects:** Shared Storage, Application Storage

Storing sensitive data unencrypted (or weakly encrypted) locally (e.g. in files, databases, caches) on device.

**Attacker goal / impact:** Storing sensitive data unencrypted on local device.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)

### Weak Server-Side Controls

**Risk:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** Elevation of Privilege

**Affects:** Application Logic

**Attacker goal / impact:** Trusting the mobile client logic too much; backend exploited.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### App Tampering or Fake Distribution Channels

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Tampering

**Affects:** App Store Client

Attackers distribute trojanized or counterfeit versions of your app outside the official App Store (e.g., via enterprise certificates or jailbroken repositories).

**Attacker goal / impact:** Distribute malware/trojans to users; revenue loss; brand damage.

**Mitigations**

- [In-App Integrity, Environment Checks, and Abuse Telemetry](mitigation-library.md#in-app-integrity-environment-checks-and-abuse-telemetry) (Preventive)
- [Signed Releases and Store-Only Distribution Controls](mitigation-library.md#signed-releases-and-store-only-distribution-controls) (Preventive)

### Broken access control

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Elevation of Privilege

**Affects:** Application Logic

An attacker could exploit broken access control to access unauthorized functionality and data, such as accessing other users' accounts, viewing sensitive files, modifying other users’ data, and changing access rights.

**Attacker goal / impact:** Access unauthorized user data or admin features; bypass restrictions.

**Mitigations**

- [Deny Access by Default](mitigation-library.md#deny-access-by-default) (Preventive)
- [Develop a comprehensive threat model](mitigation-library.md#develop-a-comprehensive-threat-model) (Preventive)
- [Enforce record ownership in models](mitigation-library.md#enforce-record-ownership-in-models) (Preventive)
- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)

### Credential Leakage

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Information Disclosure

**Affects:** Local Authentication, Credential Storage

Secrets such as API keys, tokens, or credentials could be accidentally exposed in logs or code.

**Attacker goal / impact:** Steal API keys/secrets from logs or code to attack backend.

**Mitigations**

- [Implement a secure secret management solution](mitigation-library.md#implement-a-secure-secret-management-solution) (Preventive)

### Cryptographic failure

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Information Disclosure

**Affects:** Application Logic

An attacker could exploit cryptographic failures to access sensitive data unprotected, such as credit card information, personal data, or business secrets.

**Attacker goal / impact:** Decrypt locally stored sensitive data (PII/PHI) due to weak algorithms.

**Mitigations**

- [Classify data sensitivity](mitigation-library.md#classify-data-sensitivity) (Preventive)
- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)
- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement up-to-date encryption standards](mitigation-library.md#implement-up-to-date-encryption-standards) (Preventive)

### Elevation of Privilege

**Risk:** High · **Likelihood:** Low · **Severity:** High · **Framework:** Elevation of Privilege

**Affects:** Application Logic

Elevation of privilege is when an attacker gains unauthorized access to higher-level permissions or rights within a system or application.

**Attacker goal / impact:** Gain admin or root access to the device/app logic.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)

### Identification and Authentication Failures

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Spoofing

**Affects:** Local Authentication

An attacker could exploit identification and authentication failures to impersonate legitimate users and gain unauthorized system access.

**Attacker goal / impact:** Impersonate legitimate users; bypass identity checks.

**Mitigations**

- [Change default credentials immediately](mitigation-library.md#change-default-credentials-immediately) (Preventive)
- [Enforce strong password policies](mitigation-library.md#enforce-strong-password-policies) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)

### Improper authentication

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Spoofing

**Affects:** Local Authentication

When an actor claims to have a given identity, the product does not prove or insufficiently proves that the claim is correct.

**Attacker goal / impact:** Bypass login screens; access app without valid session.

**Mitigations**

- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Injection flaws

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Tampering

**Affects:** Application Logic

An attacker could use injection flaws (like SQL, NoSQL, and OS command injection) to send hostile data to an interpreter, leading to data loss, corruption, lack of accountability, or denial of access.
 
 With SQL injection, without sufficient removal or quoting of SQL syntax in user-controllable inputs, the generated SQL query can cause those inputs to be interpreted as SQL instead of ordinary user data. This can be used to alter query logic to bypass security checks or to insert additional statements that modify the back-end database, possibly including the execution of system commands.
 
 SQL injection has become a common issue with database-driven websites. The flaw is easily detected and easily exploited. As such, any site or product package with even a minimal user base is likely to be subject to an attempted attack of this kind. This flaw depends on the fact that SQL makes no real distinction between the control and data planes.

**Attacker goal / impact:** Execute SQL/Command injection on backend or local DB.

**Mitigations**

- [Implement an ORM](mitigation-library.md#implement-an-orm) (Preventive)
- [Use safe APIs](mitigation-library.md#use-safe-apis) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Insecure Inter-Process Communication (IPC)

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Information Disclosure

**Affects:** User Interface, Application Logic

Insecure communication between apps or components can be intercepted or manipulated.

**Attacker goal / impact:** Malicious apps read data meant for your app via Intents/URL schemes.

**Mitigations**

- [Authenticated, Authorized, and Encrypted IPC Channels](mitigation-library.md#authenticated-authorized-and-encrypted-ipc-channels) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Insufficient Transport Layer Protection

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Information Disclosure

**Affects:** Application Logic

Data transmitted between the mobile app and server can be intercepted if not properly encrypted.

**Attacker goal / impact:** Man-in-the-Middle (MitM) to steal data in transit (no TLS).

**Mitigations**

- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)

### Lateral Movement

**Risk:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** Elevation of Privilege

**Affects:** Local Authentication

Expanding control over the target network beyond the initial point of compromise.

**Attacker goal / impact:** Move from compromised mobile device to backend server infrastructure.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)
- [Implement network segmentation](mitigation-library.md#implement-network-segmentation) (Preventive)

### M10: Insufficient Cryptography

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Information Disclosure

**Affects:** Application Logic

Use of weak or custom encryption algorithms, improper key management, or misuse of cryptographic primitives.

**Attacker goal / impact:** Use of deprecated crypto (MD5/SHA1) allowing data decryption.

**Mitigations**

- [Approved Algorithms, Proper Key Management, and Platform Crypto APIs](mitigation-library.md#approved-algorithms-proper-key-management-and-platform-crypto-apis) (Preventive)
- [Secure Cipher Configuration and End-to-End Data Protection](mitigation-library.md#secure-cipher-configuration-and-end-to-end-data-protection) (Preventive)

### M2: Inadequate Supply Chain Security

**Risk:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** Tampering

**Affects:** Application Logic

Vulnerabilities introduced via third-party libraries, SDKs, build tools, and the software supply chain.

**Attacker goal / impact:** Compromised 3rd party library infects all app users.

**Mitigations**

- [Secure Build Pipeline with Integrity Verification](mitigation-library.md#secure-build-pipeline-with-integrity-verification) (Preventive)
- [Vetted, Pinned, and Continuously Monitored Dependencies](mitigation-library.md#vetted-pinned-and-continuously-monitored-dependencies) (Preventive)

### M6: Inadequate Privacy Controls

**Risk:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** Information Disclosure

**Affects:** Application Storage

Poor protection of sensitive user data (personal profile, PII), improper permission use, data leaks.

**Attacker goal / impact:** Leak PII/PHI to analytics or logs; regulatory violation.

**Mitigations**

- [Implement privacy-preserving cryptographic protocols](mitigation-library.md#implement-privacy-preserving-cryptographic-protocols) (Preventive)

### M8: Security Misconfiguration

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Tampering

**Affects:** Mobile App Sandbox

Misconfigured app settings, permissions, network policies, or development/debug features left in production.

**Attacker goal / impact:** Debug features enabled in production; weak default settings.

**Mitigations**

- [Secure Build/Release Policies With Automated Misconfiguration Scanning](mitigation-library.md#secure-buildrelease-policies-with-automated-misconfiguration-scanning) (Preventive)

### Malicious Code and Malware

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Tampering

**Affects:** Application Logic

Mobile devices can be infected with malware that can compromise apps, steal data, or perform unauthorized actions.

**Attacker goal / impact:** Malware screenscrapes, keylogs, or overlays the app.

**Mitigations**

- [Download from trusted sources only](mitigation-library.md#download-from-trusted-sources-only) (Preventive)

### Missing authentication

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Spoofing

**Affects:** Application Logic

**Attacker goal / impact:** Access API endpoints or app functions without any token.

**Mitigations**

- [Implement centralized authentication](mitigation-library.md#implement-centralized-authentication) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Spoofing

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Spoofing

**Affects:** User Interface, Application Logic

**Attacker goal / impact:** Impersonate device, user, or server.

**Mitigations**

- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Tampering

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Tampering

**Affects:** User Interface, Application Logic

**Attacker goal / impact:** Modify app binary or memory to disable security checks.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement hashing for data integrity verification.](mitigation-library.md#implement-hashing-for-data-integrity-verification) (Detective)

### Vulnerable and Outdated Components

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Tampering

**Affects:** User Interface, Application Logic

**Attacker goal / impact:** Exploit known CVEs in old libraries bundled with the app.

**Mitigations**

- [Conduct Software Composition Analysis](mitigation-library.md#conduct-software-composition-analysis) (Detective)
- [Eliminate unused dependencies](mitigation-library.md#eliminate-unused-dependencies) (Preventive)
- [Source trusted libraries and packages](mitigation-library.md#source-trusted-libraries-and-packages) (Preventive)

### Client-Side Injection

**Risk:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** Tampering

**Affects:** User Interface, Application Logic

Attackers exploit vulnerabilities by injecting malicious code (e.g., JavaScript, SQL queries) into the mobile app.

**Attacker goal / impact:** Execute malicious scripts (XSS) in WebView; steal session tokens.

**Mitigations**

- [Implement Parameterization](mitigation-library.md#implement-parameterization) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Denial of Service

**Risk:** Medium · **Likelihood:** Low · **Severity:** Medium · **Framework:** Denial of Service

**Affects:** User Interface, Application Logic

Denial of service (DoS) is an attack that disrupts the normal functioning of a system or network by overwhelming it with excessive traffic or requests.

**Attacker goal / impact:** Crash the app or backend to disrupt service availability.

**Mitigations**

- [Implement Distributed Architecture](mitigation-library.md#implement-distributed-architecture) (Preventive)

### Insecure Communication with Third-Party Services

**Risk:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** Tampering

**Affects:** Application Logic

Mobile apps often interact with third-party APIs or services, which may be insecure or malicious.

**Attacker goal / impact:** Intercept or inject malicious data from compromised 3rd party APIs.

**Mitigations**

- [Develop a comprehensive threat model](mitigation-library.md#develop-a-comprehensive-threat-model) (Preventive)
- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)

### Least Privilege Principle Violation

**Risk:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** Elevation of Privilege

**Affects:** User Interface, Application Logic

An attacker breaches the deny-by-default policy, leading to potential exploitation, data breaches, or unauthorized control over system functionalities.

**Attacker goal / impact:** App requests excessive permissions (e.g., Contacts) enabling abuse.

**Mitigations**

- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)

### M4: Insufficient Input / Output Validation

**Risk:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** Tampering

**Affects:** Application Logic

Failure to properly validate, sanitize, or encode data coming into or going out of the app (leads to injections, parsing errors, etc.).

**Attacker goal / impact:** Cause app crashes, logic errors, or memory corruption.

**Mitigations**

- [Sanitize Output](mitigation-library.md#sanitize-output) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### M7: Insufficient Binary Protections

**Risk:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** Tampering

**Affects:** Mobile App Sandbox

Lack of defenses against reverse engineering, tampering, or debugging (e.g. no code obfuscation, no integrity checks).

**Attacker goal / impact:** Enable reverse engineering or runtime manipulation of code.

**Mitigations**

- [Code Obfuscation and Anti-Reverse Engineering Controls](mitigation-library.md#code-obfuscation-and-anti-reverse-engineering-controls) (Preventive)
- [Runtime Integrity, Anti-Debugging, and Tamper Detection](mitigation-library.md#runtime-integrity-anti-debugging-and-tamper-detection) (Preventive)

### Reverse Engineering

**Risk:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** Tampering

**Affects:** Application Logic

**Attacker goal / impact:** Analyze code to find vulnerabilities or steal IP.

**Mitigations**

- [Change default credentials immediately](mitigation-library.md#change-default-credentials-immediately) (Preventive)
- [Implement Code Obfuscation](mitigation-library.md#implement-code-obfuscation) (Preventive)

### Security Misconfiguration (Web and Mobile)

**Risk:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** Tampering

**Affects:** User Interface, Application Logic

**Attacker goal / impact:** Server headers/config expose info; debug ports open.

**Mitigations**

- [Harden Assets Against Attacks](mitigation-library.md#harden-assets-against-attacks) (Preventive)
- [Implement a minimal installation](mitigation-library.md#implement-a-minimal-installation) (Preventive)
- [Implement Timely Patching](mitigation-library.md#implement-timely-patching) (Corrective)

### Session Hijacking

**Risk:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** Spoofing

**Affects:** User Interface, Application Logic

**Attacker goal / impact:** Steal valid session token to impersonate user.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Secure Service Token Management](mitigation-library.md#secure-service-token-management) (Preventive)

### Side-channel data leakage

**Risk:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** Information Disclosure

**Affects:** User Interface, Application Logic

**Attacker goal / impact:** OS features (screenshots, keyboard cache) inadvertently store PII.

**Mitigations**

- [Audit Logging Configuration](mitigation-library.md#audit-logging-configuration) (Detective)

### Insecure Handling of App Store Purchase Tokens

**Risk:** Low · **Likelihood:** Medium · **Severity:** Low · **Framework:** Tampering

**Affects:** Application Logic

Storing App Store tokens, transaction IDs, or purchase receipts insecurely (e.g., in UserDefaults or unencrypted files).

**Attacker goal / impact:** Get premium features for free (Theft of Service).

**Mitigations**

- [Secure Storage and Redaction of Purchase Artifacts](mitigation-library.md#secure-storage-and-redaction-of-purchase-artifacts) (Preventive)
- [Server-Side Validation and Token Minimization](mitigation-library.md#server-side-validation-and-token-minimization) (Preventive)

### Misuse of StoreKit or App Store APIs

**Risk:** Low · **Likelihood:** Medium · **Severity:** Low · **Framework:** Tampering

**Affects:** Application Logic

**Attacker goal / impact:** Bypass payment validation; generate fake receipts.

**Mitigations**

- [Secure Handling and Minimal Exposure of StoreKit Artifacts](mitigation-library.md#secure-handling-and-minimal-exposure-of-storekit-artifacts) (Preventive)
- [Server-Side Receipt Validation and Secure StoreKit Workflows](mitigation-library.md#server-side-receipt-validation-and-secure-storekit-workflows) (Preventive)

### Receipt Forgery and Validation Attacks

**Risk:** Low · **Likelihood:** Medium · **Severity:** Low · **Framework:** Tampering

**Affects:** Application Logic

**Attacker goal / impact:** Fake a purchase receipt to unlock content.

**Mitigations**

- [Integrity-Protected Receipt Handling and Nonce Binding](mitigation-library.md#integrity-protected-receipt-handling-and-nonce-binding) (Preventive)
- [Server-Side Receipt Validation With Trusted App Store Endpoints](mitigation-library.md#server-side-receipt-validation-with-trusted-app-store-endpoints) (Preventive)

### Repudiation

**Risk:** Low · **Likelihood:** Low · **Severity:** Medium · **Framework:** Repudiation

**Affects:** Application Logic

**Attacker goal / impact:** User denies performing an action (e.g., "I didn't click that").

**Mitigations**

- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Log Security Events](mitigation-library.md#log-security-events) (Detective)
