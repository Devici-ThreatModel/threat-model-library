# Mobile App: Threats

42 curated threats, grouped by theme and ordered by priority. For full descriptions and mitigation guidance, download [mobile-app-threats-and-mitigations.csv](mobile-app-threats-and-mitigations.csv). Back to the [model overview](README.md).

## Priority summary

| Priority level | Threats |
|---|---|
| Critical | 8 |
| High | 20 |
| Medium | 10 |
| Low | 4 |

## All threats

| Threat | Framework | Likelihood | Severity | Priority | Affects | Attacker goal / impact | Recommended mitigations |
|---|---|---|---|---|---|---|---|
| **Broken Authentication** | Spoofing | High | Critical | **Critical** | Application Logic, Local Authentication | Account Takeover (ATO); impersonate legitimate users. | Deploy anti-brute force protections<br>Implement strong authentication with 2FA or MFA.<br>Map all authentication flows<br>Secure credential recovery endpoints |
| **Credential Theft** | Spoofing | High | High | **Critical** | Local Authentication | Gain valid user credentials via Phishing/Brute-force. | Eliminate one-factor authentication fallback mechanisms.<br>Implement strong authentication with 2FA or MFA. |
| **Information Disclosure** | Information Disclosure | High | High | **Critical** | User Interface, Application Logic | Leak PII/PHI to unauthorized parties via logs, storage, or net. | Encrypt all sensitive data in transit and at rest<br>Use Trusted Frameworks |
| **Insecure Data Storage** | Information Disclosure | High | High | **Critical** | Application Logic | Read sensitive files from the file system (e.g., if device is lost). | Encrypt all sensitive data in transit and at rest |
| **M1: Improper Credential Usage** | Information Disclosure | High | Critical | **Critical** | Application Logic | Hardcoded keys or weak token storage leading to full breach. | Secure Credential Storage and Removal of Hardcoded Secrets<br>Strong Credential Handling, Rotation, and Least-Privilege Access |
| **M3: Insecure Authentication / Authorization** | Spoofing | High | High | **Critical** | Application Logic | Flaws in logic allow bypassing auth or assuming roles. | Robust, Standards-Based Authentication and Secure Session Handling<br>Strict Authorization Enforcement with Server-Side Access Controls |
| **M9: Insecure Data Storage** | Information Disclosure | High | Critical | **Critical** | Shared Storage, Application Storage | Storing sensitive data unencrypted on local device. | Encrypt all sensitive data in transit and at rest |
| **Weak Server-Side Controls** | Elevation of Privilege | High | Critical | **Critical** | Application Logic | Trusting the mobile client logic too much; backend exploited. | Implement Access Control Measures<br>Use Trusted Frameworks<br>Validate User Input |
| **App Tampering or Fake Distribution Channels** | Tampering | Medium | High | **High** | App Store Client | Distribute malware/trojans to users; revenue loss; brand damage. | In-App Integrity, Environment Checks, and Abuse Telemetry<br>Signed Releases and Store-Only Distribution Controls |
| **Broken access control** | Elevation of Privilege | Medium | High | **High** | Application Logic | Access unauthorized user data or admin features; bypass restrictions. | Deny Access by Default<br>Develop a comprehensive threat model<br>Enforce record ownership in models<br>Implement Access Control Measures<br>Implement Attribute-Based Access Control (ABAC) |
| **Credential Leakage** | Information Disclosure | Medium | High | **High** | Local Authentication, Credential Storage | Steal API keys/secrets from logs or code to attack backend. | Implement a secure secret management solution |
| **Cryptographic failure** | Information Disclosure | Medium | High | **High** | Application Logic | Decrypt locally stored sensitive data (PII/PHI) due to weak algorithms. | Classify data sensitivity<br>Encrypt all data in transit using secure protocols.<br>Encrypt all sensitive data in transit and at rest<br>Implement up-to-date encryption standards |
| **Elevation of Privilege** | Elevation of Privilege | Low | High | **High** | Application Logic | Gain admin or root access to the device/app logic. | Implement Access Control Measures<br>Implement Attribute-Based Access Control (ABAC) |
| **Identification and Authentication Failures** | Spoofing | Medium | High | **High** | Local Authentication | Impersonate legitimate users; bypass identity checks. | Change default credentials immediately<br>Enforce strong password policies<br>Implement strong authentication with 2FA or MFA. |
| **Improper authentication** | Spoofing | Medium | High | **High** | Local Authentication | Bypass login screens; access app without valid session. | Use Trusted Frameworks |
| **Injection flaws** | Tampering | Medium | High | **High** | Application Logic | Execute SQL/Command injection on backend or local DB. | Implement an ORM<br>Use safe APIs<br>Validate User Input |
| **Insecure Inter-Process Communication (IPC)** | Information Disclosure | Medium | High | **High** | User Interface, Application Logic | Malicious apps read data meant for your app via Intents/URL schemes. | Authenticated, Authorized, and Encrypted IPC Channels<br>Validate User Input |
| **Insufficient Transport Layer Protection** | Information Disclosure | Medium | High | **High** | Application Logic | Man-in-the-Middle (MitM) to steal data in transit (no TLS). | Encrypt all data in transit using secure protocols. |
| **Lateral Movement** | Elevation of Privilege | Low | Critical | **High** | Local Authentication | Move from compromised mobile device to backend server infrastructure. | Implement Access Control Measures<br>Implement Attribute-Based Access Control (ABAC)<br>Implement network segmentation |
| **M10: Insufficient Cryptography** | Information Disclosure | Medium | High | **High** | Application Logic | Use of deprecated crypto (MD5/SHA1) allowing data decryption. | Approved Algorithms, Proper Key Management, and Platform Crypto APIs<br>Secure Cipher Configuration and End-to-End Data Protection |
| **M2: Inadequate Supply Chain Security** | Tampering | Low | Critical | **High** | Application Logic | Compromised 3rd party library infects all app users. | Secure Build Pipeline with Integrity Verification<br>Vetted, Pinned, and Continuously Monitored Dependencies |
| **M6: Inadequate Privacy Controls** | Information Disclosure | High | Medium | **High** | Application Storage | Leak PII/PHI to analytics or logs; regulatory violation. | Implement privacy-preserving cryptographic protocols |
| **M8: Security Misconfiguration** | Tampering | Medium | High | **High** | Mobile App Sandbox | Debug features enabled in production; weak default settings. | Secure Build/Release Policies With Automated Misconfiguration Scanning |
| **Malicious Code and Malware** | Tampering | Medium | High | **High** | Application Logic | Malware screenscrapes, keylogs, or overlays the app. | Download from trusted sources only |
| **Missing authentication** | Spoofing | Medium | High | **High** | Application Logic | Access API endpoints or app functions without any token. | Implement centralized authentication<br>Use Trusted Frameworks |
| **Spoofing** | Spoofing | Medium | High | **High** | User Interface, Application Logic | Impersonate device, user, or server. | Encrypt all data in transit using secure protocols.<br>Implement strong authentication with 2FA or MFA.<br>Use Trusted Frameworks |
| **Tampering** | Tampering | Medium | High | **High** | User Interface, Application Logic | Modify app binary or memory to disable security checks. | Encrypt all sensitive data in transit and at rest<br>Implement hashing for data integrity verification. |
| **Vulnerable and Outdated Components** | Tampering | Medium | High | **High** | User Interface, Application Logic | Exploit known CVEs in old libraries bundled with the app. | Conduct Software Composition Analysis<br>Eliminate unused dependencies<br>Source trusted libraries and packages |
| **Client-Side Injection** | Tampering | Medium | Medium | **Medium** | User Interface, Application Logic | Execute malicious scripts (XSS) in WebView; steal session tokens. | Implement Parameterization<br>Validate User Input |
| **Denial of Service** | Denial of Service | Low | Medium | **Medium** | User Interface, Application Logic | Crash the app or backend to disrupt service availability. | Implement Distributed Architecture |
| **Insecure Communication with Third-Party Services** | Tampering | Medium | Medium | **Medium** | Application Logic | Intercept or inject malicious data from compromised 3rd party APIs. | Develop a comprehensive threat model<br>Encrypt all data in transit using secure protocols. |
| **Least Privilege Principle Violation** | Elevation of Privilege | High | Medium | **Medium** | User Interface, Application Logic | App requests excessive permissions (e.g., Contacts) enabling abuse. | Implement Attribute-Based Access Control (ABAC) |
| **M4: Insufficient Input / Output Validation** | Tampering | High | Medium | **Medium** | Application Logic | Cause app crashes, logic errors, or memory corruption. | Sanitize Output<br>Validate User Input |
| **M7: Insufficient Binary Protections** | Tampering | High | Medium | **Medium** | Mobile App Sandbox | Enable reverse engineering or runtime manipulation of code. | Code Obfuscation and Anti-Reverse Engineering Controls<br>Runtime Integrity, Anti-Debugging, and Tamper Detection |
| **Reverse Engineering** | Tampering | High | Medium | **Medium** | Application Logic | Analyze code to find vulnerabilities or steal IP. | Change default credentials immediately<br>Implement Code Obfuscation |
| **Security Misconfiguration (Web and Mobile)** | Tampering | High | Medium | **Medium** | User Interface, Application Logic | Server headers/config expose info; debug ports open. | Harden Assets Against Attacks<br>Implement a minimal installation<br>Implement Timely Patching |
| **Session Hijacking** | Spoofing | Low | High | **Medium** | User Interface, Application Logic | Steal valid session token to impersonate user. | Encrypt all sensitive data in transit and at rest<br>Implement strong authentication with 2FA or MFA.<br>Secure Service Token Management |
| **Side-channel data leakage** | Information Disclosure | High | Medium | **Medium** | User Interface, Application Logic | OS features (screenshots, keyboard cache) inadvertently store PII. | Audit Logging Configuration |
| **Insecure Handling of App Store Purchase Tokens** | Tampering | Medium | Low | **Low** | Application Logic | Get premium features for free (Theft of Service). | Secure Storage and Redaction of Purchase Artifacts<br>Server-Side Validation and Token Minimization |
| **Misuse of StoreKit or App Store APIs** | Tampering | Medium | Low | **Low** | Application Logic | Bypass payment validation; generate fake receipts. | Secure Handling and Minimal Exposure of StoreKit Artifacts<br>Server-Side Receipt Validation and Secure StoreKit Workflows |
| **Receipt Forgery and Validation Attacks** | Tampering | Medium | Low | **Low** | Application Logic | Fake a purchase receipt to unlock content. | Integrity-Protected Receipt Handling and Nonce Binding<br>Server-Side Receipt Validation With Trusted App Store Endpoints |
| **Repudiation** | Repudiation | Low | Medium | **Low** | Application Logic | User denies performing an action (e.g., "I didn't click that"). | Implement strong authentication with 2FA or MFA.<br>Log Security Events |
