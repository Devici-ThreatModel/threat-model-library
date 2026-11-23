# Web Application: Threats

29 curated threats, grouped by theme and ordered by priority. Select a threat for its full description and mitigations. Back to the [model overview](README.md).

## Priority summary

| Priority level | Threats |
|---|---|
| Critical | 6 |
| High | 15 |
| Medium | 7 |
| Low | 1 |

## All threats

| Threat | Framework | Likelihood | Severity | Priority | Attacker goal / impact |
|---|---|---|---|---|---|
| [Broken Authentication](threat-details.md#broken-authentication) | Spoofing | High | Critical | **Critical** | Account Takeover (ATO); impersonate legitimate users. |
| [Broken Object Level Authorization](threat-details.md#broken-object-level-authorization) | Information Disclosure | High | Critical | **Critical** | Access other users' private data by manipulating IDs (BOLA/IDOR). |
| [Credential Theft](threat-details.md#credential-theft) | Spoofing | High | High | **Critical** | Gain valid credentials via Brute-force or Phishing to impersonate users. |
| [Information Disclosure](threat-details.md#information-disclosure) | Information Disclosure | High | High | **Critical** | Leak sensitive business data or PII to unauthorized users. |
| [Security Misconfiguration (API)](threat-details.md#security-misconfiguration-api) | Tampering | High | High | **Critical** | Exploit default passwords, debug modes, or unpatched flaws. |
| [Server Side Request Forgery (SSRF)](threat-details.md#server-side-request-forgery-ssrf) | Elevation of Privilege | Medium | Critical | **Critical** | Force the server to scan internal networks or access metadata services (cloud takeover). |
| [Broken Function Level Authorization](threat-details.md#broken-function-level-authorization) | Elevation of Privilege | Medium | High | **High** | Access administrative endpoints (e.g., /admin/delete) as a standard user. |
| [Broken Object Property Level Authorization](threat-details.md#broken-object-property-level-authorization) | Information Disclosure | Medium | High | **High** | View hidden fields (e.g., isAdmin, salary) or mass-assign values (Tampering). |
| [Broken access control](threat-details.md#broken-access-control) | Elevation of Privilege | Medium | High | **High** | Bypass restrictions to access unauthorized data or admin functions. |
| [Bypass Access Control](threat-details.md#bypass-access-control) | Elevation of Privilege | Medium | High | **High** | Force browse to hidden URLs or manipulate parameters to bypass checks. |
| [Credential Leakage](threat-details.md#credential-leakage) | Information Disclosure | Medium | High | **High** | Exposure of API keys/secrets in logs or code, leading to backend compromise. |
| [Credential Leakage or Theft](threat-details.md#credential-leakage-or-theft) | Information Disclosure | Medium | High | **High** | Secrets stolen in transit or from storage, allowing impersonation. |
| [Elevation of Privilege](threat-details.md#elevation-of-privilege) | Elevation of Privilege | Low | Critical | **High** | Gain root/admin access to the web server or application logic. |
| [Identification and Authentication Failures](threat-details.md#identification-and-authentication-failures) | Spoofing | Medium | High | **High** | Bypass identity checks to access the system anonymously or as another user. |
| [Malicious Code and Malware](threat-details.md#malicious-code-and-malware) | Tampering | Low | High | **High** | Inject malware (e.g., via file upload) to compromise the server or visitors. |
| [Missing authentication](threat-details.md#missing-authentication) | Spoofing | Medium | High | **High** | Access sensitive endpoints or resource-heavy functions without logging in. |
| [Security Logging and Monitoring Failures](threat-details.md#security-logging-and-monitoring-failures) | Repudiation | Medium | High | **High** | Delay incident response; attackers maintain persistence without detection. |
| [Session Hijacking](threat-details.md#session-hijacking) | Spoofing | Medium | High | **High** | Steal a valid session ID (via XSS or sniffing) to impersonate an active user. |
| [Software and Data Integrity Failures](threat-details.md#software-and-data-integrity-failures) | Tampering | Low | Critical | **High** | Compromise the CI/CD pipeline or update mechanism to inject malicious code. |
| [Spoofing](threat-details.md#spoofing) | Spoofing | Medium | High | **High** | Impersonate a trusted user, device, or system component. |
| [Tampering](threat-details.md#tampering) | Tampering | Medium | High | **High** | Modify data in transit or at rest to corrupt system integrity. |
| [Denial of Service](threat-details.md#denial-of-service) | Denial of Service | High | Medium | **Medium** | Overwhelm the server to make the application unavailable to legitimate users. |
| [Improper Inventory Management](threat-details.md#improper-inventory-management) | Tampering | Low | High | **Medium** | Exploit old, unpatched API versions (zombie APIs) to bypass security. |
| [Least Privilege Principle Violation](threat-details.md#least-privilege-principle-violation) | Elevation of Privilege | High | Medium | **Medium** | Exploit excessive default permissions to access data/functions not needed. |
| [Logging Failure](threat-details.md#logging-failure) | Repudiation | Medium | Medium | **Medium** | Attackers operate undetected because the system fails to record malicious events. |
| [Unrestricted Access to Sensitive Business Flows](threat-details.md#unrestricted-access-to-sensitive-business-flows) | Denial of Service | Medium | Medium | **Medium** | Abuse logic (e.g., buying all inventory, spamming comments) to damage business. |
| [Unrestricted Resource Consumption](threat-details.md#unrestricted-resource-consumption) | Denial of Service | High | Medium | **Medium** | Exhaust server CPU/Memory via complex queries or large payloads. |
| [Unsafe Consumption of APIs](threat-details.md#unsafe-consumption-of-apis) | Tampering | Low | High | **Medium** | Trusting malicious data from a 3rd party API leads to injection or compromise. |
| [Repudiation](threat-details.md#repudiation) | Repudiation | Low | Medium | **Low** | User denies performing an action (e.g., "I didn't transfer that money"). |
