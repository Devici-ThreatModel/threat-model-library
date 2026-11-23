# Web Application: Threat Details

For each threat: how the attack works, what it affects, and which mitigations counter it. Mitigation names link to the [mitigation library](mitigation-library.md). Back to the [threat list](threats.md) or the [model overview](README.md).

## All threats

### Broken Authentication

**Risk:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** Spoofing

**Affects:** API Gateway, Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service, Authentication App

Attackers could target authentication mechanisms, potentially gaining complete control of other users' accounts, accessing their data, and performing actions on their behalf.

**Attacker goal / impact:** Account Takeover (ATO); impersonate legitimate users.

**Mitigations**

- [Deploy anti-brute force protections](mitigation-library.md#deploy-anti-brute-force-protections) (Preventive)
- [Implement secure design patterns](mitigation-library.md#implement-secure-design-patterns) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Map all authentication flows](mitigation-library.md#map-all-authentication-flows) (Preventive)
- [Secure credential recovery endpoints](mitigation-library.md#secure-credential-recovery-endpoints) (Preventive)

### Broken Object Level Authorization

**Risk:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** Information Disclosure

**Affects:** API Gateway, Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service

An attacker could exploit API endpoints with broken object-level authorization by manipulating the object ID in the request, leading to unauthorized access to data.

**Attacker goal / impact:** Access other users' private data by manipulating IDs (BOLA/IDOR).

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement access control mechanisms](mitigation-library.md#implement-access-control-mechanisms) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)
- [Implement random and unpredictable record IDs](mitigation-library.md#implement-random-and-unpredictable-record-ids) (Preventive)
- [Implement record-level authorization checks for all API endpoints](mitigation-library.md#implement-record-level-authorization-checks-for-all-api-endpoints) (Preventive)

### Credential Theft

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** Spoofing

**Affects:** API Gateway

An attacker steals or guesses a password using a Brute-force attack, phishing, or credential stuffing provides the password to an AuthC that supports username/password as a fallback authentication mechanism.

**Attacker goal / impact:** Gain valid credentials via Brute-force or Phishing to impersonate users.

**Mitigations**

- [Eliminate one-factor authentication fallback mechanisms.](mitigation-library.md#eliminate-one-factor-authentication-fallback-mechanisms) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)

### Information Disclosure

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** Information Disclosure

**Affects:** API Gateway, Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service, auth_db (Postgres), user_db (Postgres), content_db (Postgres), User Database, Authentication App, Identity Provider, Log Database, Content Delivery Network

Information disclosure is the unintentional exposure or release of confidential or sensitive data to unauthorized individuals or entities.

**Attacker goal / impact:** Leak sensitive business data or PII to unauthorized users.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Security Misconfiguration (API)

**Risk:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** Tampering

**Affects:** API Gateway, Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service

Attackers might exploit unpatched flaws, services with insecure default configurations, or unprotected files and directories, potentially leading to unauthorized access or system compromise.

**Attacker goal / impact:** Exploit default passwords, debug modes, or unpatched flaws.

**Mitigations**

- [Automate configuration assessments](mitigation-library.md#automate-configuration-assessments) (Detective)
- [Harden Assets Against Attacks](mitigation-library.md#harden-assets-against-attacks) (Preventive)
- [Update configurations regularly](mitigation-library.md#update-configurations-regularly) (Corrective)

### Server Side Request Forgery (SSRF)

**Risk:** Critical · **Likelihood:** Medium · **Severity:** Critical · **Framework:** Elevation of Privilege

**Affects:** API Gateway, Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service

Attackers could exploit SSRF vulnerabilities in APIs to cause internal services enumeration, information disclosure, bypassing firewalls, or server misuse.

**Attacker goal / impact:** Force the server to scan internal networks or access metadata services (cloud takeover).

**Mitigations**

- [Deny Access by Default](mitigation-library.md#deny-access-by-default) (Preventive)
- [Disable HTTP redirections and implement a robust URL parser for client input validation.](mitigation-library.md#disable-http-redirections-and-implement-a-robust-url-parser-for-client-input-validation) (Preventive)
- [Implement network segmentation](mitigation-library.md#implement-network-segmentation) (Preventive)
- [Implement URL Validation with Allowlists](mitigation-library.md#implement-url-validation-with-allowlists) (Preventive)
- [Isolate resource fetching mechanisms within the network.](mitigation-library.md#isolate-resource-fetching-mechanisms-within-the-network) (Preventive)
- [Sanitize Output](mitigation-library.md#sanitize-output) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Broken Function Level Authorization

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Elevation of Privilege

**Affects:** API Gateway

An attacker could send legitimate API calls to endpoints they should not have access to, leading to unauthorized access to functionality and potentially service disruption.

**Attacker goal / impact:** Access administrative endpoints (e.g., /admin/delete) as a standard user.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement access control mechanisms](mitigation-library.md#implement-access-control-mechanisms) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)

### Broken Object Property Level Authorization

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Information Disclosure

**Affects:** API Gateway

An attacker could access private/sensitive object properties, potentially leading to data disclosure, corruption, or unauthorized privilege escalation.

**Attacker goal / impact:** View hidden fields (e.g., isAdmin, salary) or mass-assign values (Tampering).

**Mitigations**

- [Implement property-level access controls](mitigation-library.md#implement-property-level-access-controls) (Preventive)
- [Implement schema-based response validation](mitigation-library.md#implement-schema-based-response-validation) (Preventive)
- [Limit property exposure](mitigation-library.md#limit-property-exposure) (Preventive)

### Broken access control

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Elevation of Privilege

**Affects:** Authentication App

An attacker could exploit broken access control to access unauthorized functionality and data, such as accessing other users' accounts, viewing sensitive files, modifying other users’ data, and changing access rights.

**Attacker goal / impact:** Bypass restrictions to access unauthorized data or admin functions.

**Mitigations**

- [Deny Access by Default](mitigation-library.md#deny-access-by-default) (Preventive)
- [Enforce record ownership in models](mitigation-library.md#enforce-record-ownership-in-models) (Preventive)
- [Implement access control mechanisms](mitigation-library.md#implement-access-control-mechanisms) (Preventive)

### Bypass Access Control

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Elevation of Privilege

**Affects:** API Gateway

As an attacker, I aim to bypass access control checks by modifying the URL via parameter tampering or force browsing, altering the internal application state, manipulating the HTML page, or using specialized attack tools to modify API requests.

**Attacker goal / impact:** Force browse to hidden URLs or manipulate parameters to bypass checks.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Credential Leakage

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Information Disclosure

**Affects:** API Gateway

Secrets such as API keys, tokens, or credentials could be accidentally exposed in logs or code.

**Attacker goal / impact:** Exposure of API keys/secrets in logs or code, leading to backend compromise.

**Mitigations**

- [Implement a secure secret management solution](mitigation-library.md#implement-a-secure-secret-management-solution) (Preventive)

### Credential Leakage or Theft

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Information Disclosure

**Affects:** SMS / Text Code

Secrets such as API keys, tokens, or credentials could be accidentally exposed in logs or code, or stolen in transit.

**Attacker goal / impact:** Secrets stolen in transit or from storage, allowing impersonation.

**Mitigations**

- [Decommission the use of text messages](mitigation-library.md#decommission-the-use-of-text-messages) (Preventive)
- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)

### Elevation of Privilege

**Risk:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** Elevation of Privilege

**Affects:** API Gateway, Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service, Authentication App, Identity Provider, Content Delivery Network

Elevation of privilege is when an attacker gains unauthorized access to higher-level permissions or rights within a system or application.

**Attacker goal / impact:** Gain root/admin access to the web server or application logic.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)

### Identification and Authentication Failures

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Spoofing

**Affects:** Identity Provider

An attacker could exploit identification and authentication failures to impersonate legitimate users and gain unauthorized system access.

**Attacker goal / impact:** Bypass identity checks to access the system anonymously or as another user.

**Mitigations**

- [Change default credentials immediately](mitigation-library.md#change-default-credentials-immediately) (Preventive)
- [Enforce strong password policies](mitigation-library.md#enforce-strong-password-policies) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)

### Malicious Code and Malware

**Risk:** High · **Likelihood:** Low · **Severity:** High · **Framework:** Tampering

**Affects:** Browser

Mobile devices can be infected with malware that can compromise apps, steal data, or perform unauthorized actions.

**Attacker goal / impact:** Inject malware (e.g., via file upload) to compromise the server or visitors.

**Mitigations**

- [Use anti-virus and anti-malware software](mitigation-library.md#use-anti-virus-and-anti-malware-software) (Preventive)

### Missing authentication

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Spoofing

**Affects:** API Gateway, Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service, Authentication App, Identity Provider

The product does not perform any authentication for functionality that requires a provable user identity or consumes a significant amount of resources.

**Attacker goal / impact:** Access sensitive endpoints or resource-heavy functions without logging in.

**Mitigations**

- [Implement centralized authentication](mitigation-library.md#implement-centralized-authentication) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Security Logging and Monitoring Failures

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Repudiation

**Affects:** Log Database

An attacker could leverage insufficient logging and monitoring to carry out attacks without being detected, hindering security incident identification and response.

**Attacker goal / impact:** Delay incident response; attackers maintain persistence without detection.

**Mitigations**

- [Implement a Security Information and Event Management (SIEM) solution.](mitigation-library.md#implement-a-security-information-and-event-management-siem-solution) (Detective)
- [Implement Comprehensive Logging](mitigation-library.md#implement-comprehensive-logging) (Detective)
- [Log Security Events](mitigation-library.md#log-security-events) (Detective)

### Session Hijacking

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Spoofing

**Affects:** Identity Provider, Browser

An attacker discovers/compromises the session management strategy and gains access to an object by impersonating another user or a service.

**Attacker goal / impact:** Steal a valid session ID (via XSS or sniffing) to impersonate an active user.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Secure Service Token Management](mitigation-library.md#secure-service-token-management) (Preventive)

### Software and Data Integrity Failures

**Risk:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** Tampering

**Affects:** Content Delivery Network

An attacker could exploit software and data integrity failures, such as assuming trust in the integrity of software updates, critical data, and CI/CD pipelines without verification.

**Attacker goal / impact:** Compromise the CI/CD pipeline or update mechanism to inject malicious code.

**Mitigations**

- [Conduct Software Composition Analysis](mitigation-library.md#conduct-software-composition-analysis) (Detective)
- [Implement digital signatures for integrity verification](mitigation-library.md#implement-digital-signatures-for-integrity-verification) (Preventive)
- [Utilize trusted repositories for libraries and dependencies](mitigation-library.md#utilize-trusted-repositories-for-libraries-and-dependencies) (Preventive)

### Spoofing

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Spoofing

**Affects:** API Gateway, Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service, Authentication App, Identity Provider, Content Delivery Network

Spoofing is where an attacker masquerades as a trusted entity to gain unauthorized access or deceive recipients.

**Attacker goal / impact:** Impersonate a trusted user, device, or system component.

**Mitigations**

- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Tampering

**Risk:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** Tampering

**Affects:** API Gateway, Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service, auth_db (Postgres), user_db (Postgres), content_db (Postgres), User Database, Authentication App, Identity Provider, Log Database, Content Delivery Network

Tampering with data involves unauthorized changes to digital information, often with harmful intent, making it unreliable and leading to serious consequences.

**Attacker goal / impact:** Modify data in transit or at rest to corrupt system integrity.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement hashing for data integrity verification.](mitigation-library.md#implement-hashing-for-data-integrity-verification) (Detective)
- [Protect against malicious updates to CDN](mitigation-library.md#protect-against-malicious-updates-to-cdn) (Preventive)

### Denial of Service

**Risk:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** Denial of Service

**Affects:** API Gateway, Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service, auth_db (Postgres), user_db (Postgres), content_db (Postgres), User Database, Authentication App, Identity Provider, Log Database, Content Delivery Network

Denial of service (DoS) is an attack that disrupts the normal functioning of a system or network by overwhelming it with excessive traffic or requests.

**Attacker goal / impact:** Overwhelm the server to make the application unavailable to legitimate users.

**Mitigations**

- [Implement Distributed Architecture](mitigation-library.md#implement-distributed-architecture) (Preventive)

### Improper Inventory Management

**Risk:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** Tampering

**Affects:** API Gateway, Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service

Attackers could gain unauthorized access through old API versions, unpatched endpoints, or third parties with weaker security, leading to data leaks or server takeover.

**Attacker goal / impact:** Exploit old, unpatched API versions (zombie APIs) to bypass security.

**Mitigations**

- [Automate API documentation generation and restrict access to authorized users only](mitigation-library.md#automate-api-documentation-generation-and-restrict-access-to-authorized-users-only) (Preventive)
- [Catalog integrated services and their data handling](mitigation-library.md#catalog-integrated-services-and-their-data-handling) (Preventive)
- [Document API endpoints](mitigation-library.md#document-api-endpoints) (Preventive)

### Least Privilege Principle Violation

**Risk:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** Elevation of Privilege

**Affects:** Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service, Authentication App

An attacker breaches the deny-by-default policy, leading to potential exploitation, data breaches, or unauthorized control over system functionalities.

**Attacker goal / impact:** Exploit excessive default permissions to access data/functions not needed.

**Mitigations**

- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)
- [Implement secure design patterns](mitigation-library.md#implement-secure-design-patterns) (Preventive)

### Logging Failure

**Risk:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** Repudiation

**Affects:** auth_db (Postgres), user_db (Postgres), content_db (Postgres), User Database, Log Database

An attacker can attack the App Server, and because it does not log at the correct level, the Response team is unaware of the attack.​

**Attacker goal / impact:** Attackers operate undetected because the system fails to record malicious events.

**Mitigations**

- [Audit Logging Configuration](mitigation-library.md#audit-logging-configuration) (Detective)
- [Implement a Security Information and Event Management (SIEM) solution.](mitigation-library.md#implement-a-security-information-and-event-management-siem-solution) (Detective)
- [Implement Comprehensive Logging](mitigation-library.md#implement-comprehensive-logging) (Detective)

### Unrestricted Access to Sensitive Business Flows

**Risk:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** Denial of Service

**Affects:** API Gateway

Attackers could exploit sensitive business flows in APIs, causing harm such as preventing legitimate users from purchasing a product or leading to inflation in a game's internal economy.

**Attacker goal / impact:** Abuse logic (e.g., buying all inventory, spamming comments) to damage business.

**Mitigations**

- [Block Non-Human Traffic](mitigation-library.md#block-non-human-traffic) (Preventive)
- [Implement CAPTCHA for User Verification](mitigation-library.md#implement-captcha-for-user-verification) (Preventive)
- [Implement device fingerprinting to block unauthorized client devices](mitigation-library.md#implement-device-fingerprinting-to-block-unauthorized-client-devices) (Preventive)

### Unrestricted Resource Consumption

**Risk:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** Denial of Service

**Affects:** API Gateway, Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service, auth_db (Postgres), user_db (Postgres), content_db (Postgres), User Database, Identity Provider, Log Collector, Log Database

Attackers could exploit unrestricted resource consumption, leading to DoS due to resource starvation or increased operational costs.

**Attacker goal / impact:** Exhaust server CPU/Memory via complex queries or large payloads.

**Mitigations**

- [Implement API rate limiting](mitigation-library.md#implement-api-rate-limiting) (Preventive)
- [Implement resource limits](mitigation-library.md#implement-resource-limits) (Preventive)
- [Limit parameter and payload sizes](mitigation-library.md#limit-parameter-and-payload-sizes) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Unsafe Consumption of APIs

**Risk:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** Tampering

**Affects:** API Gateway, Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service

Attackers might identify and compromise other APIs/services integrated with the target API, leading to sensitive information exposure, injections, or denial of service.

**Attacker goal / impact:** Trusting malicious data from a 3rd party API leads to injection or compromise.

**Mitigations**

- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)
- [Evaluate service provider API security](mitigation-library.md#evaluate-service-provider-api-security) (Preventive)
- [Validate and sanitize API inputs](mitigation-library.md#validate-and-sanitize-api-inputs) (Preventive)

### Repudiation

**Risk:** Low · **Likelihood:** Low · **Severity:** Medium · **Framework:** Repudiation

**Affects:** API Gateway, Authentication & Authorization Service, User Profile / Account Service, Content / Domain Data Service, auth_db (Postgres), user_db (Postgres), content_db (Postgres), User Database, Authentication App, Identity Provider, Log Database, Browser, Content Delivery Network

Repudiation is the rejection or denial of a performed action.

**Attacker goal / impact:** User denies performing an action (e.g., "I didn't transfer that money").

**Mitigations**

- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Log Security Events](mitigation-library.md#log-security-events) (Detective)
