# Mobile App: Threats

42 curated threats, grouped by theme and ordered by risk. Select a threat for its full description and mitigations. Back to the [model overview](README.md).

## Risk summary

| Risk level | Threats |
|---|---|
| Critical | 8 |
| High | 20 |
| Medium | 10 |
| Low | 4 |

## All threats

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Broken Authentication](threat-details.md#broken-authentication) | Spoofing | High | Critical | **Critical** | Account Takeover (ATO); impersonate legitimate users. |
| [Credential Theft](threat-details.md#credential-theft) | Spoofing | High | High | **Critical** | Gain valid user credentials via Phishing/Brute-force. |
| [Information Disclosure](threat-details.md#information-disclosure) | Information Disclosure | High | High | **Critical** | Leak PII/PHI to unauthorized parties via logs, storage, or net. |
| [Insecure Data Storage](threat-details.md#insecure-data-storage) | Information Disclosure | High | High | **Critical** | Read sensitive files from the file system (e.g., if device is lost). |
| [M1: Improper Credential Usage](threat-details.md#m1-improper-credential-usage) | Information Disclosure | High | Critical | **Critical** | Hardcoded keys or weak token storage leading to full breach. |
| [M3: Insecure Authentication / Authorization](threat-details.md#m3-insecure-authentication--authorization) | Spoofing | High | High | **Critical** | Flaws in logic allow bypassing auth or assuming roles. |
| [M9: Insecure Data Storage](threat-details.md#m9-insecure-data-storage) | Information Disclosure | High | Critical | **Critical** | Storing sensitive data unencrypted on local device. |
| [Weak Server-Side Controls](threat-details.md#weak-server-side-controls) | Elevation of Privilege | High | Critical | **Critical** | Trusting the mobile client logic too much; backend exploited. |
| [App Tampering or Fake Distribution Channels](threat-details.md#app-tampering-or-fake-distribution-channels) | Tampering | Medium | High | **High** | Distribute malware/trojans to users; revenue loss; brand damage. |
| [Broken access control](threat-details.md#broken-access-control) | Elevation of Privilege | Medium | High | **High** | Access unauthorized user data or admin features; bypass restrictions. |
| [Credential Leakage](threat-details.md#credential-leakage) | Information Disclosure | Medium | High | **High** | Steal API keys/secrets from logs or code to attack backend. |
| [Cryptographic failure](threat-details.md#cryptographic-failure) | Information Disclosure | Medium | High | **High** | Decrypt locally stored sensitive data (PII/PHI) due to weak algorithms. |
| [Elevation of Privilege](threat-details.md#elevation-of-privilege) | Elevation of Privilege | Low | High | **High** | Gain admin or root access to the device/app logic. |
| [Identification and Authentication Failures](threat-details.md#identification-and-authentication-failures) | Spoofing | Medium | High | **High** | Impersonate legitimate users; bypass identity checks. |
| [Improper authentication](threat-details.md#improper-authentication) | Spoofing | Medium | High | **High** | Bypass login screens; access app without valid session. |
| [Injection flaws](threat-details.md#injection-flaws) | Tampering | Medium | High | **High** | Execute SQL/Command injection on backend or local DB. |
| [Insecure Inter-Process Communication (IPC)](threat-details.md#insecure-inter-process-communication-ipc) | Information Disclosure | Medium | High | **High** | Malicious apps read data meant for your app via Intents/URL schemes. |
| [Insufficient Transport Layer Protection](threat-details.md#insufficient-transport-layer-protection) | Information Disclosure | Medium | High | **High** | Man-in-the-Middle (MitM) to steal data in transit (no TLS). |
| [Lateral Movement](threat-details.md#lateral-movement) | Elevation of Privilege | Low | Critical | **High** | Move from compromised mobile device to backend server infrastructure. |
| [M10: Insufficient Cryptography](threat-details.md#m10-insufficient-cryptography) | Information Disclosure | Medium | High | **High** | Use of deprecated crypto (MD5/SHA1) allowing data decryption. |
| [M2: Inadequate Supply Chain Security](threat-details.md#m2-inadequate-supply-chain-security) | Tampering | Low | Critical | **High** | Compromised 3rd party library infects all app users. |
| [M6: Inadequate Privacy Controls](threat-details.md#m6-inadequate-privacy-controls) | Information Disclosure | High | Medium | **High** | Leak PII/PHI to analytics or logs; regulatory violation. |
| [M8: Security Misconfiguration](threat-details.md#m8-security-misconfiguration) | Tampering | Medium | High | **High** | Debug features enabled in production; weak default settings. |
| [Malicious Code and Malware](threat-details.md#malicious-code-and-malware) | Tampering | Medium | High | **High** | Malware screenscrapes, keylogs, or overlays the app. |
| [Missing authentication](threat-details.md#missing-authentication) | Spoofing | Medium | High | **High** | Access API endpoints or app functions without any token. |
| [Spoofing](threat-details.md#spoofing) | Spoofing | Medium | High | **High** | Impersonate device, user, or server. |
| [Tampering](threat-details.md#tampering) | Tampering | Medium | High | **High** | Modify app binary or memory to disable security checks. |
| [Vulnerable and Outdated Components](threat-details.md#vulnerable-and-outdated-components) | Tampering | Medium | High | **High** | Exploit known CVEs in old libraries bundled with the app. |
| [Client-Side Injection](threat-details.md#client-side-injection) | Tampering | Medium | Medium | **Medium** | Execute malicious scripts (XSS) in WebView; steal session tokens. |
| [Denial of Service](threat-details.md#denial-of-service) | Denial of Service | Low | Medium | **Medium** | Crash the app or backend to disrupt service availability. |
| [Insecure Communication with Third-Party Services](threat-details.md#insecure-communication-with-third-party-services) | Tampering | Medium | Medium | **Medium** | Intercept or inject malicious data from compromised 3rd party APIs. |
| [Least Privilege Principle Violation](threat-details.md#least-privilege-principle-violation) | Elevation of Privilege | High | Medium | **Medium** | App requests excessive permissions (e.g., Contacts) enabling abuse. |
| [M4: Insufficient Input / Output Validation](threat-details.md#m4-insufficient-input--output-validation) | Tampering | High | Medium | **Medium** | Cause app crashes, logic errors, or memory corruption. |
| [M7: Insufficient Binary Protections](threat-details.md#m7-insufficient-binary-protections) | Tampering | High | Medium | **Medium** | Enable reverse engineering or runtime manipulation of code. |
| [Reverse Engineering](threat-details.md#reverse-engineering) | Tampering | High | Medium | **Medium** | Analyze code to find vulnerabilities or steal IP. |
| [Security Misconfiguration (Web and Mobile)](threat-details.md#security-misconfiguration-web-and-mobile) | Tampering | High | Medium | **Medium** | Server headers/config expose info; debug ports open. |
| [Session Hijacking](threat-details.md#session-hijacking) | Spoofing | Low | High | **Medium** | Steal valid session token to impersonate user. |
| [Side-channel data leakage](threat-details.md#side-channel-data-leakage) | Information Disclosure | High | Medium | **Medium** | OS features (screenshots, keyboard cache) inadvertently store PII. |
| [Insecure Handling of App Store Purchase Tokens](threat-details.md#insecure-handling-of-app-store-purchase-tokens) | Tampering | Medium | Low | **Low** | Get premium features for free (Theft of Service). |
| [Misuse of StoreKit or App Store APIs](threat-details.md#misuse-of-storekit-or-app-store-apis) | Tampering | Medium | Low | **Low** | Bypass payment validation; generate fake receipts. |
| [Receipt Forgery and Validation Attacks](threat-details.md#receipt-forgery-and-validation-attacks) | Tampering | Medium | Low | **Low** | Fake a purchase receipt to unlock content. |
| [Repudiation](threat-details.md#repudiation) | Repudiation | Low | Medium | **Low** | User denies performing an action (e.g., "I didn't click that"). |
