# Mobile App: Mitigation Library

59 distinct mitigations, listed once each in alphabetical order, with the threats each one addresses. Back to the [threat details](threat-details.md) or the [model overview](README.md).

Control categories: **Preventive** stops an attack, **Detective** spots one in progress, **Corrective** limits damage and restores service.

## Approved Algorithms, Proper Key Management, and Platform Crypto APIs

*Preventive*

Use only industry-standard, vetted cryptographic algorithms (AES-GCM, SHA-256, ECC) through platform-provided libraries, and enforce strong key management practices including hardware-backed storage (Secure Enclave / Keystore), non-exportable keys, and rotation policies to prevent misuse of weak or custom cryptography.

**Addresses:** [M10: Insufficient Cryptography](threat-details.md#m10-insufficient-cryptography)

## Audit Logging Configuration

*Detective*

Audit logging configuration to ensure all relevant events are logged at the appropriate level. Regularly review logs for completeness and accuracy, and verify that sensitive data is not exposed. Ensure logs are sent to the SIEM for monitoring and alerting. Implement controls to prevent unauthorized access to logs and related data.

**How to implement:**

- Define logging levels clearly to distinguish between critical, warning, and informational events.
- implement Log rotation and retention policies to manage Log size and ensure timely review.
- Use encryption for logs, especially those containing sensitive Information, to prevent unauthorized access.
- regularly Train staff on logging best practices and the importance of data protection.
- Establish incident response protocols for when logging anomalies are detected.

**Why it works:** The system captures events based on defined logging levels, ensuring critical incidents are logged with high priority. Logs are structured to separate sensitive data from general information, utilizing data masking techniques. Logs are encrypted during transmission and storage. Automated tools analyze logs for anomalies, and alerts are generated for suspicious activities. Log access is restricted to authorized personnel only, with regular audits to ensure compliance and effectiveness.

**Examples:**

- Splunk: Log analysis and alerting
- ELK Stack: logging and visualization
- Graylog: Real-time Log Management
- HashiCorp Vault: secure Log storage
- IBM QRadar and Microsoft Sentinel: SIEM solutions with anomaly detection

**Addresses:** [Side-channel data leakage](threat-details.md#side-channel-data-leakage)

## Authenticated, Authorized, and Encrypted IPC Channels

*Preventive*

Use OS-backed secure IPC mechanisms (e.g., named pipes, domain sockets, platform IPC frameworks) with mutual authentication, strict ACLs, and transport encryption so only authorized processes can establish IPC channels and eavesdropping or tampering on messages is prevented.

**Addresses:** [Insecure Inter-Process Communication (IPC)](threat-details.md#insecure-inter-process-communication-ipc)

## Change default credentials immediately

*Preventive*

Change all default credentials for admin and user accounts immediately. Implement strong, unique passwords for each account to prevent unauthorized access.

**How to implement:**

- Identify all accounts using factory-default credentials
- Change default usernames and passwords during initial setup
- Use tools or scripts to Enforce password changes upon first login
- Remove or Disable default accounts that are not needed
- Apply secure, unique passwords when replacing default credentials - verify that no systems are deployed with hardcoded or unchanged defaults

**Why it works:** Default credentials are widely known and often exploited in attacks. Systems should enforce immediate credential changes upon deployment or initial login. All default admin and user accounts must be reviewed and updated with strong, unique passwords. Where possible, default accounts should be removed entirely. Automating detection and enforcement of credential changes reduces risk and helps prevent unauthorized access due to overlooked defaults.

**Examples:**

- OS hardening scripts (e.g., Ansible, PowerShell DSC): automate credential resets on first Boot
- AWS IAM access Analyzer: Flags accounts using default or overly permissive credentials
- Dockerfile best practices: Recommend overriding default credentials at container Build time
- OpenVAS / Nessus: detect systems using known default credentials during Scans

**Addresses:** [Identification and Authentication Failures](threat-details.md#identification-and-authentication-failures); [Reverse Engineering](threat-details.md#reverse-engineering)

## Classify data sensitivity

*Preventive*

Classify data based on its sensitivity level (such as public, internal, confidential, or restricted) and apply appropriate controls for each category. This ensures that sensitive information is handled securely, meets compliance requirements, and is protected from unauthorized access or disclosure.

**How to implement:**

- Define clear classification tiers based on regulatory, legal, and business risk factors.
- Train personnel to recognize and handle each classification level correctly.
- Use automated tools to detect, label, and tag sensitive data across systems.
- Enforce different access control policies and encryption requirements per data class.
- Review and update classification schemes regularly based on evolving risks.
- Monitor access to sensitive data and generate alerts on anomalous activity.

**Why it works:** Data classification involves identifying and labeling information based on its sensitivity and risk level. This process enables organizations to apply the correct security controls to different types of data, such as encryption, access restrictions, and audit logging. Automated classification tools streamline enforcement by tagging sensitive information in real time. Ongoing monitoring and access reviews help detect misuse and support compliance obligations.

**Examples:**

- Symantec DLP for automatic classification and protection
- Microsoft Information protection for tagging and access control
- AWS Macie for discovering and labeling sensitive data in cloud storage
- VeraCrypt for encrypting sensitive files
- HashiCorp Vault for classified data Key Management
- IBM Guardium for monitoring access to protected data

**Addresses:** [Cryptographic failure](threat-details.md#cryptographic-failure)

## Code Obfuscation and Anti-Reverse Engineering Controls

*Preventive*

Apply platform-appropriate code obfuscation, symbol stripping, and resource hardening, and enable anti-reverse engineering protections (class/method renaming, string encryption, control-flow obfuscation) to make it significantly harder for attackers to analyze, clone, or modify the app binary.

**Addresses:** [M7: Insufficient Binary Protections](threat-details.md#m7-insufficient-binary-protections)

## Conduct Software Composition Analysis

*Detective*

Regularly assess and update all software components, libraries, and frameworks to the latest secure versions. Implement automated checks for vulnerabilities and ensure all software updates are verified for integrity before deployment.

**How to implement:**

- Use SCA tools to detect vulnerable third-party components.
- Define policies for managing component updates and acceptable license types.
- Integrate SCA into CI/CD pipelines to trigger checks automatically.
- track software bill of materials (SBOM) to improve visibility of Open-source use.
- Educate developers on selecting well-maintained, secure libraries.
- verify software integrity using cryptographic signatures when available.

**Why it works:** Software Composition Analysis (SCA) identifies known vulnerabilities in third-party libraries and open-source components. By integrating SCA into the CI/CD pipeline, organizations can detect risks early and enforce policies for safe and compliant component use. SCA tools help maintain visibility over software supply chains and alert teams to security, license, or integrity concerns, enabling timely updates and reducing risk.

**Examples:**

- Snyk: Scans open-source dependencies for vulnerabilities and license risks.
- OWASP Dependency-Check: Identifies known vulnerable components in Java and .NET.
- GitHub Dependabot: Scans for outdated libraries and creates update pull requests.
- Docker Content Trust: Verifies container image integrity using digital signatures.
- Veracode SCA: Detects and manages risks in third-party libraries.
- JFrog Xray: Analyzes binaries and enforces open-source policies.

**Addresses:** [Vulnerable and Outdated Components](threat-details.md#vulnerable-and-outdated-components)

## Deny Access by Default

*Preventive*

Enforce a deny-by-default access control policy, where no user, system, or plugin is granted access unless explicitly allowed by defined rules. Default behavior should reject all requests until specific permissions are granted through access policies or allow-lists.

**How to implement:**

- Define explicit allow-lists for all actions, users, services, and data access.
- Configure default access controls to deny any request unless explicitly authorized.
- ensure all new plugins, APIs, and user roles are evaluated for access restrictions before deployment.
- Review access control configurations regularly to ensure no implicit permissions exist.
- Enforce access policies through infrastructure-as-code or configuration Management to prevent misconfigurations.

**Why it works:** Deny-by-default policies ensure that access is never assumed or open by default. Instead, each access request must meet pre-approved conditions before being granted. This limits the potential attack surface and prevents unauthorized interactions. By configuring allow-lists and enforcing explicit permissions at every layer—from API gateways to internal services, organizations prevent unintended access. Regular audits help detect and remove outdated or overly permissive rules.

**Examples:**

- AWS IAM: IAM policies can be configured to deny all access unless specifically allowed via policies.
- Google Cloud IAM uses allow-based roles where no access is granted until explicitly permitted.
- API Gateways: Only routes explicitly defined in the gateway are reachable; others are denied by default.
- Azure Resource Manager enforces deny-by-default behavior in RBAC assignments.
- Kubernetes Network Policies deny all pod-to-pod communication by default unless allow-rules are defined.

**Addresses:** [Broken access control](threat-details.md#broken-access-control)

## Deploy anti-brute force protections

*Preventive*

Implement anti-brute force protections at all authentication endpoints to prevent unauthorized access. This includes account lockout policies, rate limiting, and CAPTCHA challenges after a specified number of failed login attempts.

**How to implement:**

- implement account lockout policies to temporarily Disable accounts after failed login attempts
- Apply rate limiting to Restrict repeated login attempts from the same source within a short timeframe
- Use CAPTCHA challenges after multiple failed attempts to block automated attacks - implement IP blacklisting for persistent attackers
- Monitor and Log login attempts for suspicious patterns - test the effectiveness of protections through simulated attacks

**Why it works:** To defend against brute-force attacks, authentication endpoints must enforce layered protections. Account lockout policies temporarily disable access after repeated failures, while rate limiting restricts login attempts in a short timeframe. CAPTCHA challenges stop automated tools, and IP blacklisting blocks persistent attackers. Logging and regular testing ensure these controls remain effective against evolving threats.

**Examples:**

- Cloudflare Bot Management: Enforces rate limiting and CAPTCHA after failed attempts
- Google reCAPTCHA: Blocks automated login attempts using challenge-response
- AWS WAF: Supports IP-based login throttling and blocking rules
- Fail2Ban: Analyzes logs and blacklists IPs after repeated failures
- Okta: Implements lockout policies and multi-Layer login defenses
- Microsoft Azure AD: Provides account lockout, CAPTCHA, and adaptive risk-based controls

**Addresses:** [Broken Authentication](threat-details.md#broken-authentication)

## Develop a comprehensive threat model

*Preventive*

Identify and evaluate potential threats to systems by analyzing assets, attack surfaces, and vulnerabilities. Develop a structured threat model to understand how attackers could exploit weaknesses and to prioritize risks. Use this model to inform future security design and decision-making.

**How to implement:**

- Identify assets, users, and data flows
- Map attack surfaces and trust boundaries
- Enumerate threats using frameworks like STRIDE or MITRE ATT&CK - assess likelihood and impact for risk prioritization
- Involve cross-functional teams (Security, dev, ops)
- update the model regularly to reflect system changes

**Why it works:** Threat modeling involves identifying system assets, mapping how data flows between components, and evaluating how attackers might exploit vulnerabilities. Teams use frameworks like STRIDE to classify threats and assess risks. The model guides secure design and helps prioritize mitigations based on potential impact.

**Examples:**

- Devici for structured threat modeling and risk analysis
- SD Elements (SDE) for integrating threat modeling into secure development workflows
- MITRE ATT&CK for identifying and mapping adversary techniques
- Draw.io or Lucidchart for visualizing system architecture and data flow

**Addresses:** [Broken access control](threat-details.md#broken-access-control); [Insecure Communication with Third-Party Services](threat-details.md#insecure-communication-with-third-party-services)

## Download from trusted sources only

*Preventive*

Only download apps and files from reputable and verified sources to minimize the risk of malware infections.

**How to implement:**

- verify the source of apps and files before downloading, ensuring they originate from official stores or trusted vendors.
- Avoid third-party app stores and unknown websites.
- Check developer reputation, app reviews, and download counts.
- confirm apps are signed and validated by the platform’s Security mechanisms.
- Educate users to Avoid pirated or cracked apps.

**Why it works:** Downloading only from trusted sources minimizes exposure to malicious software. Verified app stores use vetting mechanisms such as code reviews, digital signatures, and reputation systems to ensure authenticity and safety. Avoiding unofficial or pirated sources helps prevent malware infections, credential theft, and unauthorized data access.

**Examples:**

- Play protect: Scans all installs, warns on malicious apps, and will Automatically Disable harmful ones.
- F‑Droid Implements signature verification and reproducible builds, allowing for robust source trust.
- Avoid third-party APK sites and pirated apps due to high malware risk

**Addresses:** [Malicious Code and Malware](threat-details.md#malicious-code-and-malware)

## Eliminate one-factor authentication fallback mechanisms.

*Preventive*

Identify and remove all one-factor authentication fallback mechanisms from the system. Ensure that all authentication processes require multi-factor authentication to enhance security. Regularly audit the system to detect and eliminate any remaining fallback options.

**How to implement:**

- Audit systems to identify and disable fallback authentication methods (e.g., password-only or SMS-only)
- Enforce MFA as the sole method for all user logins
- Block login attempts that do not include valid MFA tokens
- Configure IAM policies to prevent bypass of MFA
- Educate users on secure MFA usage
- Regularly test and update systems to close fallback routes

**Why it works:** The system must be designed to enforce multi-factor authentication (MFA) as the sole method for user access. This includes integrating authentication methods such as time-based one-time passwords (TOTPs), biometric verification, or hardware tokens. All user accounts should be configured to reject any login attempts that do not provide the required MFA. Regular audits should be conducted to ensure no fallback options exist, and any legacy systems must be updated to comply with this requirement.

**Examples:**

- Examples of technology that implement this mitigation include Google Authenticator for TOTP, YubiKey for hardware-based MFA, Microsoft Authenticator for app-based verification, and biometric systems like fingerprint or facial recognition on devices. Additionally, services like Duo Security and Okta provide comprehensive MFA solutions that enforce multi-factor authentication without fallback options.

**Addresses:** [Credential Theft](threat-details.md#credential-theft)

## Eliminate unused dependencies

*Preventive*

Remove all unused dependencies and features from your software components to reduce potential attack surfaces. Regularly audit and update remaining components to ensure they are current and secure.

**How to implement:**

- implement automated tools to Identify and Remove unused dependencies.
- Establish a regular Schedule for Dependency audits and updates.
- Utilize Dependency Management tools to track versions and vulnerabilities.
- Educate developers on the risks of excessive dependencies.
- Promote minimalistic, well-maintained libraries to reduce complexity.

**Why it works:** Eliminating unused dependencies reduces the attack surface by removing unnecessary code and libraries. Automated tools can scan for unused components during builds, while regular audits ensure outdated or insecure packages are addressed. Dependency managers help track versions and vulnerabilities, and ongoing monitoring promotes secure, lean development practices.

**Examples:**

- npm Audit: Identifies and reports vulnerabilities in Node.js dependencies.
- Bundler: a Ruby tool to manage and clean unused gems.
- Gradle: Supports removal of unused Java dependencies during builds.
- Dependabot: Automatically updates and Helps clean unused GitHub dependencies.
- SonarQube: detects unused code and libraries in various languages.
- Depcheck: Scans JavaScript projects for unused or missing dependencies.

**Addresses:** [Vulnerable and Outdated Components](threat-details.md#vulnerable-and-outdated-components)

## Encrypt all data in transit using secure protocols.

*Preventive*

Encrypt all data in transit using current, secure communication protocols such as TLS 1.3. Ensure all services and APIs are authenticated and data is encrypted between endpoints to protect against interception and tampering. Validate implementation against cryptographic best practices, and avoid deprecated or insecure protocols. Regularly review and update configurations to maintain data integrity and confidentiality.

**How to implement:**

- Use strong, modern encryption protocols (e.g., TLS 1.3) and secure cipher suites.
- Implement certificate pinning to protect against man-in-the-middle (MITM) attacks.
- Ensure third-party libraries and dependencies related to cryptography are kept up to date.
- Conduct regular audits and penetration tests to verify secure implementation of encryption in transit.
- Use mutual TLS (mTLS) where appropriate to authenticate both client and server.

**Why it works:** Securing data in transit involves encrypting all communications between clients, servers, and third-party systems using modern protocols like TLS 1.3. Certificate pinning strengthens MITM defenses, while mutual TLS ensures both endpoints are authenticated. Keeping libraries updated prevents the use of known-vulnerable cryptographic methods. Regular testing and validation confirm correct implementation and allow prompt remediation of weaknesses in encrypted communication paths.

**Examples:**

- TLS 1.3 for end-to-end encrypted communication
- HTTPS for secure web traffic
- Mutual TLS (mTLS) for API authentication
- Certificate pinning in mobile apps
- OpenSSL for implementing strong cryptographic protocols
- Cloudflare WAF to inspect and secure encrypted traffic
- VPNs for encrypted connections to external systems

**Addresses:** [Cryptographic failure](threat-details.md#cryptographic-failure); [Insecure Communication with Third-Party Services](threat-details.md#insecure-communication-with-third-party-services); [Insufficient Transport Layer Protection](threat-details.md#insufficient-transport-layer-protection); [Spoofing](threat-details.md#spoofing)

## Encrypt all sensitive data in transit and at rest

*Preventive*

Encrypt all sensitive data both in transit and at rest to protect it from unauthorized access. Implement strong encryption protocols for data flows crossing trust boundaries and ensure that sensitive information is stored securely using encryption methods that meet industry standards.

**How to implement:**

- Use strong encryption protocols (e.g., TLS 1.2+, AES-256) and avoid weak or outdated algorithms
- Encrypt data stored on disks, databases, and backups
- Apply encryption to data in transit across internal and external networks
- Ensure encryption is enabled by default in systems handling sensitive data
- Ensure encryption keys are securely managed and rotated regularly

**Why it works:** Sensitive data should be encrypted both at rest and in transit using strong protocols like AES-256 and TLS 1.2+. Encryption must be applied to all data crossing trust boundaries, such as between services or across networks. Keys should be stored securely and rotated regularly. Avoid weak algorithms and ensure encryption settings follow industry best practices by default.

**Examples:**

- AES (Advanced encryption Standard) for encrypting data at rest
- TLS (Transport Layer Security) for securing data in transit
- AWS Key Management Service (KMS) for secure Key Management
- Microsoft Azure Disk encryption for encrypting virtual machine disks
- VeraCrypt for creating encrypted containers for sensitive files
- BitLocker for encrypting entire drives on Windows devices

**Addresses:** [Cryptographic failure](threat-details.md#cryptographic-failure); [Information Disclosure](threat-details.md#information-disclosure); [Insecure Data Storage](threat-details.md#insecure-data-storage); [M9: Insecure Data Storage](threat-details.md#m9-insecure-data-storage); [Session Hijacking](threat-details.md#session-hijacking); [Tampering](threat-details.md#tampering)

## Enforce record ownership in models

*Preventive*

Implement strict ownership checks in your data models to ensure users can only access their own records. Validate user permissions at the model level to prevent unauthorized access to functionality and data.

**How to implement:**

- Apply ownership checks at all access layers, including APIs, services, and UI.
- Use unique user identifiers to associate records with owners.
- Employ RBAC to Define and Enforce access boundaries based on ownership.
- Log access attempts and Monitor for violations or anomalies.
- regularly Review access rules to reflect changes in user roles or system structure.
- Provide secure coding guidelines to help developers implement consistent ownership checks.

**Why it works:** Record ownership enforcement involves linking each data entry to a specific user and validating ownership before granting access. This check should be implemented at the model or middleware level to ensure it applies regardless of how data is accessed. Role-based access controls (RBAC) can refine permissions to only allow users to interact with their own records. Ownership checks must be applied consistently across all components, with logging and alerting to detect unauthorized access attempts.

**Examples:**

- AWS IAM: Enables permissions based on ownership of specific resources.
- OAuth 2.0: Scopes access tokens to user-specific data, enforcing ownership.
- Django: Uses mixins and decorators to restrict views to owner’s records.
- Microsoft Azure AD: Supports RBAC to enforce access rules at resource levels.
- Spring Security: Supports annotations for method-level ownership checks in Java apps.

**Addresses:** [Broken access control](threat-details.md#broken-access-control)

## Enforce strong password policies

*Preventive*

Implement strong password policies that require complex passwords, regular updates, and prohibit commonly used passwords. Enforce multi-factor authentication for all user accounts to enhance security and prevent unauthorized access. Regularly review and update authentication mechanisms to align with current best practices.

**How to implement:**

- Require passwords to Include a mix of upper and lower case letters, numbers, and special characters.
- implement account lockout mechanisms after a certain number of failed login attempts.
- Educate users on recognizing phishing attempts and the importance of password security.
- Utilize password managers to encourage unique passwords for different accounts.
- regularly Audit user accounts for inactive or unnecessary access rights.

**Why it works:** Strong password policies protect against brute-force and credential stuffing attacks. Enforce complexity rules, prohibit commonly used or reused passwords, and require periodic password changes. Account lockout after failed attempts adds further protection. Tools like password managers help users maintain secure, unique passwords. Regular audits ensure users comply with the defined password policy and reduce the risk of compromise.

**Examples:**

- Microsoft Azure Active Directory: Enforces strong password policies and supports MFA
- Okta Identity Cloud: Offers adaptive MFA and password policy enforcement
- LastPass: Helps users generate, store, and use strong passwords
- Google Workspace: Provides 2-Step Verification and password protections - 1Password: Encourages secure and unique password use across accounts

**Addresses:** [Identification and Authentication Failures](threat-details.md#identification-and-authentication-failures)

## Harden Assets Against Attacks

*Preventive*

Apply security best practices to reduce vulnerabilities in systems, applications, and infrastructure. This includes disabling unused services, enforcing strong configurations, patching known issues, and limiting exposed interfaces to minimize the attack surface.

**How to implement:**

- Identify and Prioritize critical assets
- Disable unnecessary ports, services, and default accounts
- Apply secure configuration baselines (e.g., CIS Benchmarks) -regularly patch systems and software
- Use configuration Management tools for consistency
- Monitor for configuration drift and misconfigurations - document and standardize hardening procedures for repeatability

**Why it works:** Hardening reduces the likelihood of compromise by minimizing exposure points attackers could exploit. This involves securing default configurations, limiting access, and maintaining consistent baselines across environments. It supports defense-in-depth by strengthening each component before it's exposed to internal or external threats.

**Examples:**

- Use AWS systems Manager or Azure Policy for config enforcement
- Apply CIS Benchmarks for Windows, Linux, or cloud services
- Use Ansible, Chef, or Puppet for consistent hardening
- Disable unused services in EC2, GCE, or VMware instances
- Apply Security Groups/firewall rules in AWS, Azure, or GCP
- Use Amazon Inspector or Azure Defender for vulnerability Scans - patch using WSUS, SCCM, or Linux Package managers

**Addresses:** [Security Misconfiguration (Web and Mobile)](threat-details.md#security-misconfiguration-web-and-mobile)

## Implement a minimal installation

*Preventive*

Use a minimal installation approach by configuring only essential features and frameworks. Regularly review and remove any unused components, files, and directories.

**How to implement:**

- Identify and install Only essential packages, services, and dependencies.
- Remove default applications, modules, and libraries not required for operation.
- Validate that updates don’t reintroduce unused or insecure features.

**Why it works:** Minimal installation starts with a secure baseline configuration containing only essential components, reducing the attack surface. Automated compliance checks and regular audits help detect misconfigurations.

**Examples:**

- Ansible can automate minimal package installs using roles and playbooks. Terraform defines infrastructure with only required resources, avoiding defaults.

**Addresses:** [Security Misconfiguration (Web and Mobile)](threat-details.md#security-misconfiguration-web-and-mobile)

## Implement a secure secret management solution

*Preventive*

Store all credentials in a secure, encrypted secret management solution, ensuring they are not hard-coded in the application. Restrict access to these secrets to authorized components only, and regularly audit for potential credential leakage in logs and code.

**How to implement:**

- Choose a secret Management solution that Fits your architecture and operational needs
- Apply environment-specific configurations to isolate secrets by stage - ensure secrets are rotated regularly using automated processes
- Monitor and Audit secret access for unusual activity
- Educate developers on secure handling of secrets and available tooling

**Why it works:** A secure secret management solution stores sensitive credentials in an encrypted vault. Applications access these secrets through secure APIs, avoiding exposure in code or config files. Permissions control access, while logging and audits track usage. Regular rotation and monitoring help reduce the risk of leaks and ensure secrets remain up to date.

**Examples:**

- HashiCorp Vault: centralized tool for encrypted secret storage
- AWS secrets Manager: manages and rotates secrets in AWS
- Azure Key Vault: stores and secures secrets, keys, and certs
- CyberArk Conjur: Open-source tool for app and user secret access
- Google secret Manager: Google’s Vault for keys, certs, and tokens

**Addresses:** [Credential Leakage](threat-details.md#credential-leakage)

## Implement Access Control Measures

*Preventive*

Implement robust access control mechanisms to validate and authorize each entity's actions within the system. Ensure that permissions are strictly enforced to prevent unauthorized access to sensitive data and functionality. Regularly review and update access controls to address vulnerabilities and adhere to the principle of least privilege.

**How to implement:**

- Define clear access policies based on job responsibilities and data sensitivity
- Use least privilege as a default for all roles and permissions
- Separate duties across roles to reduce risk from over-privileged accounts
- Review and update access rights regularly, especially after role changes
- Apply fine-grained access control at the resource, function, and data level

**Why it works:** Access control ensures users and systems only access what they need based on roles and responsibilities. By applying least privilege and separating duties, organizations reduce the risk of abuse or error. Fine-grained controls restrict access to specific data or functions, and regular reviews ensure permissions stay aligned with evolving roles.

**Examples:**

- AWS IAM / Azure RBAC: Define and manage granular role-based access
- Okta / Keycloak: Centralize user role Management and access policies
- OPA (Open Policy Agent): Enforce fine-grained access at the application level
- GitLab / GitHub roles: control project and repository access by role
- GCP IAM Conditions: Apply attribute-based access rules for resources

**Addresses:** [Broken access control](threat-details.md#broken-access-control); [Elevation of Privilege](threat-details.md#elevation-of-privilege); [Lateral Movement](threat-details.md#lateral-movement); [Weak Server-Side Controls](threat-details.md#weak-server-side-controls)

## Implement an ORM

*Preventive*

Implement an ORM to abstract database operations, enabling secure, consistent query generation. This reduces SQL injection risk by preventing manual query string construction and centralizing data handling logic.

**How to implement:**

- Choose a well-maintained ORM that Supports parameterization.
- Apply patches to known ORM vulnerabilities promptly.
- limit direct database access and Enforce usage policies.
- Train developers in ORM-specific Security practices.

**Why it works:** ORMs encapsulate database interaction logic, automatically binding user input as data. This prevents direct SQL construction and supports centralized data validation. Using ORM-specific best practices reduces the attack surface of database queries.

**Examples:**

- Examples of ORMs that implement this mitigation include: 1. Entity Framework (for .NET applications) 2. Hibernate (for Java applications) 3. Django ORM (for Python applications) 4. Sequelize (for Node.js applications) 5. ActiveRecord (for Ruby on Rails applications) These ORMs support parameterized queries and provide built-in mechanisms for input sanitization, thereby reducing the risk of SQL injection vulnerabilities.

**Addresses:** [Injection flaws](threat-details.md#injection-flaws)

## Implement Attribute-Based Access Control (ABAC)

*Preventive*

Implement Attribute-Based Access Control (ABAC) to enforce access decisions based on user attributes like role, location, and resource characteristics. Ensure that access is granted only to authorized users, preventing lateral movement, privilege escalation, and unauthorized access to functions or data.

**How to implement:**

- ensure attributes used for access control are accurate and up-to-date to prevent unauthorized access.
- implement logging and monitoring of access requests to detect and respond to anomalies.
- regularly Audit access policies to Identify and rectify potential gaps or misconfigurations.
- Use multi-factor authentication (MFA) to strengthen access control.
- Educate users on the importance of attribute accuracy and the risks of privilege escalation.

**Why it works:** ABAC implementation involves defining user attributes, resource characteristics, and environmental conditions to create access policies. These policies evaluate attributes dynamically at the time of access requests, ensuring that only users meeting specific criteria can access resources. The system utilizes a policy engine to process requests, applying rules that reflect the least privilege principle. Regular audits and real-time monitoring ensure the detection of unauthorized access attempts.

**Examples:**

- Examples of technology that implement Attribute-Based Access Control (ABAC) include
- AWS Identity and Access Management (IAM)
- Azure Active Directory Conditional Access
- Okta Identity Cloud
- Google Cloud IAM.
- Solutions like Axiomatics Policy Server and Auth0 provide ABAC capabilities. These technologies allow for dynamic access control based on user attributes and contextual information.

**Addresses:** [Broken access control](threat-details.md#broken-access-control); [Elevation of Privilege](threat-details.md#elevation-of-privilege); [Lateral Movement](threat-details.md#lateral-movement); [Least Privilege Principle Violation](threat-details.md#least-privilege-principle-violation)

## Implement centralized authentication

*Preventive*

Implement a centralized authentication system across your application to ensure all user identity verification is consistent and secure.

**How to implement:**

- Choose a centralized authentication system that supports standard protocols such as OAuth 2.0, OpenID Connect, or SAML to ensure broad compatibility and secure identity federation.
- Integrate single sign-on (SSO) capabilities to streamline user access across multiple services while maintaining centralized control.
- Centralize user identity management to simplify role assignments, access control, and audit logging across all service

**Why it works:** Centralized authentication uses a single service to manage user identities, enforce access policies, and support secure login across systems. Standard protocols like OAuth 2.0 and SAML enable integration, while SSO reduces user friction. Central identity management ensures consistent role enforcement, simplifies audits, and improves security through centralized monitoring.

**Examples:**

- Azure Active Directory: Supports SSO and integrates with Microsoft services.
- Google Identity Platform: Provides authentication services using OAuth 2.0
- AWS Cognito: Enables user sign-up, sign-in, and access control for web and mobile apps.
- Okta: Cloud-based identity service with OAuth and SAML support.
- Auth0: Developer-friendly platform for centralized authentication.
- Keycloak: Open-source identity broker with role-based access control.

**Addresses:** [Missing authentication](threat-details.md#missing-authentication)

## Implement Code Obfuscation

*Preventive*

Use code obfuscation techniques to make your mobile app's source and machine code difficult to interpret.

**How to implement:**

- Choose robust Obfuscation tools that are regularly updated to counter new reverse engineering techniques.
- combine Obfuscation with other Security measures, such as encryption and secure coding practices, for layered protection.
- regularly evaluate the effectiveness of Obfuscation methods against current reverse engineering tools.
- Educate developers on the importance of secure coding and Obfuscation practices.

**Why it works:** Code obfuscation transforms readable source code into a harder-to-understand version without changing its behavior. This makes reverse engineering more difficult. It typically includes renaming identifiers, altering control flow, and inserting dummy code. Automated build tools help integrate obfuscation into development pipelines, and regular updates ensure resistance to evolving analysis methods.

**Examples:**

- ProGuard: A tool for Android that shrinks, optimizes, and obfuscates code.
- DexGuard: An advanced version of ProGuard with extra Android security.
- R8: A modern code shrinker and obfuscator for Android apps.
- ConfuserEx: An open-source .NET obfuscator.
- JavaGuard: A Java obfuscator to prevent reverse engineering.
- DashO: A commercial tool for Java and Android with advanced obfuscation.

**Addresses:** [Reverse Engineering](threat-details.md#reverse-engineering)

## Implement Distributed Architecture

*Preventive*

Deploy multiple instances of your application across different servers to ensure horizontal scaling and improve resilience against Denial of Service attacks.

**How to implement:**

- Utilize load balancers to distribute incoming traffic evenly across instances.
- implement auto-scaling to dynamically adjust resources based on traffic spikes.
- implement redundancy in server locations to prevent single points of failure.
- Use caching mechanisms to reduce load on application servers.
- Monitor traffic patterns to Identify and respond to potential DoS attempts quickly.
- regularly test the architecture for vulnerabilities and performance under stress.

**Why it works:** Deploy services across multiple nodes and regions to eliminate single points of failure. Use load balancers to evenly distribute traffic and auto-scaling to adjust compute capacity dynamically. Integrate caching layers to optimize performance and monitor traffic patterns to detect and mitigate DoS attacks in real time. It should be complemented with a strong incident response program to ensure quick detection, investigation, and recovery from disruptions.

**Examples:**

- Examples of technology that implement a distributed architecture include
- Amazon Web Services (AWS) Elastic Load Balancing
- Google Cloud Load Balancing
- Microsoft Azure Load Balancer for traffic distribution.
- Kubernetes can manage containerized applications across multiple nodes, while Cloudflare and Akamai provide content delivery networks (CDNs) that cache content and absorb traffic spikes.
- Redis or Memcached can be used for caching to reduce server load.

**Addresses:** [Denial of Service](threat-details.md#denial-of-service)

## Implement hashing for data integrity verification.

*Detective*

Use cryptographic hash functions to generate unique hash digests for all critical data inputs. Regularly compare these digests against stored values to detect unauthorized changes or data poisoning.

**How to implement:**

- Select strong, collision-resistant hash functions (e.g., SHA-256).
- Store hash digests securely, separate from the data they verify, to prevent tampering.
- Implement regular audits of hash comparisons to ensure ongoing integrity checks.
- Use a secure key management system for any keys involved in hashing processes.
- Integrate hashing with access control mechanisms to prevent unauthorized data submissions.
- Educate staff on recognizing and responding to integrity alerts.

**Why it works:** Implement a system where each critical data input is processed through a secure cryptographic hash function, generating a unique hash digest. Store these digests in a secure, isolated environment. Establish a routine that regularly compares current data against stored digests, triggering alerts upon discrepancies. Integrate this process with access control to block unauthorized submissions and ensure staff are trained to respond to integrity alerts effectively.

**Examples:**

- Blockchain technology, which uses hashing to ensure the integrity of transactions and blocks.
- Git version control system, which employs SHA-1 hashes to verify file integrity and track changes.
- Database systems like PostgreSQL that can use hash functions for data integrity checks on critical tables.
- File integrity monitoring tools such as Tripwire, which utilize hashing to detect unauthorized changes to files.

**Addresses:** [Tampering](threat-details.md#tampering)

## Implement network segmentation

*Preventive*

Implement network segmentation to create subnets with access controls to minimize exposure. It can be used to isolate critical systems and limit lateral movement. Ensure that different segments have controlled access based on roles and functions, and restrict server-side requests to only necessary endpoints to mitigate SSRF risks, and monitor for unauthorized access attempts across segments.

**How to implement:**

- Define clear access controls for each segment based on least privilege principles.
- Utilize firewalls and intrusion detection systems to Monitor traffic between segments.
- regularly conduct penetration testing to Identify weaknesses in segmentation.
- implement logging and alerting for unusual access patterns across segments.
- Use API Gateways to Enforce strict validation and Sanitization of incoming requests.
- Educate staff on the importance of network segmentation and SSRF risks.

**Why it works:** Design implementation involves creating distinct network segments for different functions, such as production, development, and testing, with strict access controls. Each segment employs firewalls to filter traffic and intrusion detection systems to monitor for anomalies. SSRF mitigation includes whitelisting allowed endpoints and using API gateways for request validation. Regular reviews and updates of segmentation policies, along with logging and alerting mechanisms, ensure ongoing security.

**Examples:**

- Examples of technology that implement network segmentation include:
- VMware NSX for micro-segmentation
- Cisco ACI for application-centric infrastructure
- Palo Alto Networks firewalls for traffic control. For SSRF mitigation, tools to enforce request validation and restrict server-side requests to approved endpoints.:
- AWS Lambda with VPC endpoints
- API management solutions like Apigee
- Web application firewalls (WAFs) such as AWS WAF

**Addresses:** [Lateral Movement](threat-details.md#lateral-movement)

## Implement Parameterization

*Preventive*

Use parameterized queries and prepared statements to enforce strict separation of code and data in database and OS operations, preventing injection attacks. Ensure input values are bound to placeholders rather than concatenated into code strings.

**How to implement:**

- Enforce Use of parameterized APIs or libraries for all command and database operations.
- Audit codebases to Identify and eliminate unsafe string concatenation.
- Validate all input values before binding them to parameters.
- ensure consistent Use of prepared statements in both backend and frontend frameworks.
- regularly test parameter handling through code reviews and Security audits.

**Why it works:** Parameterization works by clearly separating user input from the command or query structure. Instead of injecting input directly into commands, parameters are used as placeholders, which prevents injection attacks. This technique ensures inputs are interpreted strictly as data, not executable code. Regular audits and validations help maintain its effectiveness, especially in preventing OS and database-level injection threats.

**Examples:**

- For OS Command Injection, libraries like Apache Commons Exec and Python's subprocess module provide methods to safely execute commands with parameters.
- In Python, use the subprocess.run(["cmd", param]) pattern.
- In Java, use PreparedStatement to bind variables in SQL queries.
- In web apps, frameworks like React escape inputs in templates, and libraries like DOMPurify sanitize HTML.
- Use ORMs like SQLAlchemy or Entity Framework to enforce parameterization automatically.

**Addresses:** [Client-Side Injection](threat-details.md#client-side-injection)

## Implement privacy-preserving cryptographic protocols

*Preventive*

Use privacy-preserving cryptographic protocols to secure communication and data processing while minimizing data exposure. Prioritize methods such as homomorphic encryption, secure multi-party computation (SMC), and zero-knowledge proofs (ZKPs) to protect sensitive data during operations. Regularly update protocols to address evolving threats.

**How to implement:**

- Use Homomorphic encryption to compute on encrypted data.
- implement secure multi-party computation (SMC) to collaborate without exposing inputs.
- Apply ZKPs for private verification.
- Utilize Oblivious Transfer for anonymous data exchange.
- incorporate differential privacy to protect query responses.
- Use private set intersection for safe data comparison.

**Why it works:** Privacy-preserving cryptographic protocols allow data to remain confidential during processing and communication. Homomorphic encryption enables computation on encrypted data. SMC lets parties jointly compute without revealing inputs. ZKPs verify facts without exposing them. Oblivious transfer hides which data was shared. These methods support secure, private data workflows.

**Examples:**

- Microsoft SEAL: Implements Homomorphic encryption for secure computation.
- MP-SPDZ: a framework for secure multi-party computation.
- Zokrates: ZKP toolkit for smart contracts on Ethereum.
- Obliv-'C': Programming language for Oblivious Transfer and secure computation.
- OpenDP: Implements differential privacy in statistical analysis.
- PSI by Facebook/OpenMined: Enables private set intersection for contact discovery.

**Addresses:** [M6: Inadequate Privacy Controls](threat-details.md#m6-inadequate-privacy-controls)

## Implement strong authentication with 2FA or MFA.

*Preventive*

Implement Two-Factor Authentication (2FA) or Multi-Factor Authentication (MFA) to enhance identity verification for all users.

**How to implement:**

- Select authentication methods that combine at least two distinct factors (e.g., password + TOTP or hardware token)
- Require biometric factors where possible for enhanced security.
- Support widely adopted authenticators like TOTP apps or FIDO2 devices
- Enforce MFA for all users, especially for privileged accounts
- Ensure fallback mechanisms are secure and limited

**Why it works:** Strong authentication with 2FA or MFA uses two or more factors—like passwords and TOTP apps or hardware tokens—to verify user identity. Even if a password is compromised, a second factor helps prevent unauthorized access. MFA should be enforced across all login flows, including admin panels and APIs, to reduce the risk of account takeover and credential-based attacks.

**Examples:**

- Google / Microsoft Authenticator: TOTP apps for 2FA
- YubiKey / SoloKey: Hardware tokens using FIDO2/U2F
- Duo Security: Enterprise MFA with multiple factor types
- GitHub / AWS / Salesforce: Offer built-in MFA enforcement
- Authy: Cross-device TOTP support with cloud sync

**Addresses:** [Broken Authentication](threat-details.md#broken-authentication); [Credential Theft](threat-details.md#credential-theft); [Identification and Authentication Failures](threat-details.md#identification-and-authentication-failures); [Repudiation](threat-details.md#repudiation); [Session Hijacking](threat-details.md#session-hijacking); [Spoofing](threat-details.md#spoofing)

## Implement Timely Patching

*Corrective*

Establish a robust patch management process to ensure timely updates for critical security components. Regularly monitor for vulnerabilities and apply patches immediately upon release. Prioritize patching based on severity and impact to maintain the integrity of your architecture.

**How to implement:**

- automate patch deployment to reduce errors and improve speed.
- Have a rollback plan for failed patches.
- Train staff on secure patching practices.

**Why it works:** Automated patch deployment reduces delays and minimizes human error, ensuring faster remediation of vulnerabilities. A rollback plan is essential to restore system stability in case a patch introduces issues. Training staff on secure patching practices increases awareness and ensures that updates are applied effectively without compromising system integrity or availability.

**Examples:**

- WSUS (Windows server update services): Automates patch distribution across Windows environments.
- Ansible: Enables automated deployment and rollback of patches across servers.
- JFrog Artifactory: Tracks and manages third-party Package versions for updates.
- Azure update Manager / AWS systems Manager patch Manager: Automates patching in cloud infrastructure.
- Qualys patch Management: Provides automation, rollback options, and patch compliance tracking.

**Addresses:** [Security Misconfiguration (Web and Mobile)](threat-details.md#security-misconfiguration-web-and-mobile)

## Implement up-to-date encryption standards

*Preventive*

Apply the latest industry-approved encryption standards to protect sensitive data. Ensure cryptographic algorithms, protocols, and key management practices are regularly updated to mitigate emerging threats and comply with evolving security requirements.

**How to implement:**

- Periodically assess encryption configurations to ensure compliance with current standards (e.g., NIST, ISO).
- Replace outdated algorithms (e.g., SHA-1, RSA-1024) with modern, secure alternatives (e.g., AES-256, SHA-3, ECC).
- Enforce key rotation schedules and ensure use of strong, unique keys.
- Monitor regulatory and vendor guidance for updates to approved encryption protocols.
- Train developers on proper use of cryptographic libraries and deprecation timelines.

**Why it works:** Keeping encryption mechanisms up to date requires continuous monitoring of cryptographic standards and replacing deprecated algorithms. This includes migrating from older protocols like TLS 1.1 to secure versions like TLS 1.3, using secure key lengths, and leveraging services that automatically adopt current best practices. Up-to-date encryption strengthens resilience against known exploits and ensures compliance with regulatory frameworks such as GDPR, HIPAA, or PCI-DSS.

**Examples:**

- AWS KMS: Supports AES-256 and automatic key rotation.
- Azure Key Vault: Uses FIPS 140-2 validated modules.
- Google Cloud Encryption: Enforces TLS 1.3, supports customer-managed keys.
- OpenSSL 3.x: Includes modern cipher suites.
- Cloudflare: Uses TLS 1.3 for secure web traffic.
- Apple CryptoKit: Offers current encryption APIs for iOS/macOS.

**Addresses:** [Cryptographic failure](threat-details.md#cryptographic-failure)

## In-App Integrity, Environment Checks, and Abuse Telemetry

*Preventive*

Implement runtime integrity checks (jailbreak/root detection, signature validation, tamper checks) and telemetry that flags or blocks execution on compromised devices or untrusted builds, enabling detection and response when counterfeit or modified app versions are used in the wild.

**Addresses:** [App Tampering or Fake Distribution Channels](threat-details.md#app-tampering-or-fake-distribution-channels)

## Integrity-Protected Receipt Handling and Nonce Binding

*Preventive*

Bind receipts to transaction-specific nonces and device identifiers, and store them only in secure platform storage while checking integrity (signature, bundle ID, product ID) on each use, blocking replayed or altered receipts from passing validation.

**Addresses:** [Receipt Forgery and Validation Attacks](threat-details.md#receipt-forgery-and-validation-attacks)

## Log Security Events

*Detective*

Implement logging for all security-relevant events to ensure traceability of user and attacker actions. Log access attempts, changes to sensitive data, and system alerts. Regularly review and analyze logs to detect anomalies and support incident response.

**How to implement:**

- ensure logs are tamper-proof and stored securely to prevent unauthorized alterations.
- implement Log retention policies that comply with regulatory requirements.
- Use standardized formats for logs to facilitate analysis and correlation.
- Establish alerting mechanisms for anomalous activities detected in logs.
- Train staff on the importance of logging and how to interpret logs for incident response.

**Why it works:** Implement a centralized logging system to capture all security-relevant events across the infrastructure. Use cryptographic techniques to make logs tamper-evident and ensure they are time-stamped for precise event sequencing. Secure log storage with restricted access, and integrate with a SIEM for real-time analysis and alerting. Conduct regular audits and retain logs for a defined period to support forensic investigations.

**Examples:**

- Examples of technology that implement comprehensive logging include
- SIEM (Security Information and Event Management) solutions like Splunk and IBM QRadar, which aggregate and analyze logs from various sources.
- Cloud services like AWS CloudTrail provide detailed logging of API calls.
- Tools like Graylog and ELK Stack (Elasticsearch, Logstash, Kibana) enable centralized log management and analysis, ensuring traceability and compliance with retention policies.

**Addresses:** [Repudiation](threat-details.md#repudiation)

## Map all authentication flows

*Preventive*

Identify and document all authentication flows across the system, including APIs, web, and mobile entry points. Include methods used (e.g., OAuth, SAML), token generation and expiration practices, and secure password storage. Regularly review and update this documentation to mitigate risks from broken or outdated authentication mechanisms.

**How to implement:**

- Identify all entry points where authentication occurs, including APIs, Web apps, and mobile platforms.
- document the methods used for authentication and how credentials or tokens are validated.
- Include token expiration policies, refresh flows, and storage mechanisms.
- verify password storage practices Use secure hashing algorithms.
- update the documentation regularly to reflect system changes or new access points.
- Involve relevant teams to Validate completeness and accuracy

**Why it works:** Mapping authentication flows is essential to identify hidden entry points that could be exploited by attackers. Without a full inventory, it's easy to overlook outdated, duplicated, or misconfigured flows that increase the risk of credential misuse or session hijacking. A clear map improves visibility, simplifies risk analysis, and supports more effective access control and incident response planning.

**Examples:**

- Use Postman + Auth logs (e.g., CloudTrail, SIEM) to manually trace Real authentication journeys.
- Use IAM platforms to visualize configured flows.
- Use Burp/ZAP to catch any hidden or forgotten endpoints during red teaming.

**Addresses:** [Broken Authentication](threat-details.md#broken-authentication)

## Robust, Standards-Based Authentication and Secure Session Handling

*Preventive*

Use proven authentication standards (OIDC / OAuth2), enforce MFA where appropriate, and protect tokens with secure storage, short lifetimes, refresh rotation, and TLS-only transport to prevent credential replay, session hijacking, or unauthorized reuse of authentication artifacts.

**Addresses:** [M3: Insecure Authentication / Authorization](threat-details.md#m3-insecure-authentication--authorization)

## Runtime Integrity, Anti-Debugging, and Tamper Detection

*Preventive*

Implement runtime checks for debugging, hooking, and tampering (debugger attachment, unexpected code injection, signature or checksum mismatch) and fail securely or limit functionality when a compromised or modified environment is detected, reducing the impact of binary manipulation in the wild.

**Addresses:** [M7: Insufficient Binary Protections](threat-details.md#m7-insufficient-binary-protections)

## Sanitize Output

*Preventive*

Sanitize all output to eliminate dangerous characters and prevent execution of arbitrary commands, XSS, and SSRF vulnerabilities. Ensure that any user-generated content is properly validated and encoded before being processed or displayed. Implement strict input validation and output encoding practices to mitigate risks associated with command injection and cross-site scripting.

**How to implement:**

- implement a whitelist approach for allowed characters and commands.
- Use libraries or frameworks that Automatically handle output encoding.
- regularly Review and update Sanitization rules based on emerging threats.
- Monitor logs for unusual patterns indicating attempted exploitation.
- conduct regular Security audits and penetration testing focused on output handling.
- Educate developers on secure coding practices related to output sanitization.

**Why it works:** Sanitize all output by implementing a robust filtering mechanism that removes or encodes potentially dangerous characters. Use a whitelist approach for allowed characters and commands, and leverage established libraries for output encoding. Ensure user-generated content is validated against strict criteria before processing. Regularly update sanitization rules and conduct security audits to identify and address vulnerabilities. Monitor logs for unusual activity to detect exploitation attempts.

**Examples:**

- OWASP Java Encoder: Escapes user output to prevent XSS
- DOMPurify: XSS sanitizer for HTML and SVG
- Joi/Validator.js: Enforce output input/output validation
- Cloudflare/AWS WAF: Blocks SSRF and encoded exploits
- Content Security Policy (CSP): limits executable output sources

**Addresses:** [M4: Insufficient Input / Output Validation](threat-details.md#m4-insufficient-input--output-validation)

## Secure Build Pipeline with Integrity Verification

*Preventive*

Protect the CI/CD pipeline with signed source, reproducible builds, artifact integrity checks, and developer identity controls, ensuring that build tools and third-party components cannot be replaced, injected, or modified within the software supply chain.

**Addresses:** [M2: Inadequate Supply Chain Security](threat-details.md#m2-inadequate-supply-chain-security)

## Secure Build/Release Policies With Automated Misconfiguration Scanning

*Preventive*

Enforce CI/CD checks that scan for insecure settings (debug flags, logging levels, plaintext traffic, exported components) and validate platform security requirements before release, preventing misconfigured builds or permissive policies from reaching production users.

**Addresses:** [M8: Security Misconfiguration](threat-details.md#m8-security-misconfiguration)

## Secure Cipher Configuration and End-to-End Data Protection

*Preventive*

Enforce correct cryptographic configurations (authenticated encryption modes, random IVs, sufficient key sizes) and apply encryption consistently to all sensitive data in transit and at rest, ensuring that no plaintext or improperly protected data is left exposed within the application or device environment.

**Addresses:** [M10: Insufficient Cryptography](threat-details.md#m10-insufficient-cryptography)

## Secure credential recovery endpoints

*Preventive*

Implement strong security measures for credential recovery endpoints, including rate limiting, CAPTCHA, and multi-factor authentication. Ensure that recovery processes verify user identity rigorously and log all recovery attempts for monitoring and auditing.

**How to implement:**

- ensure recovery links expire after a short duration to prevent misuse.
- implement email or SMS verification for any changes to recovery information.
- Use unique, unpredictable tokens for recovery processes to prevent enumeration attacks.
- regularly Review and update recovery procedures to address emerging threats.
- Educate users on recognizing phishing attempts related to recovery processes.

**Why it works:** Credential recovery endpoints must enforce secure practices to prevent abuse. Recovery links should expire quickly to reduce the risk of reuse. Each recovery attempt should generate a unique, unpredictable token to prevent guessing or enumeration. Any change to recovery information should trigger email or SMS-based verification. Regular reviews ensure recovery workflows stay updated, while user training helps prevent phishing and social engineering attacks.

**Examples:**

- Google account recovery: uses MFA and token-based verification with expiration
- Authy: Sends SMS codes for recovery verification
- LastPass: Implements CAPTCHA, rate limiting, and email verification for changes
- Okta: Provides secure, customizable identity recovery workflows
- Microsoft Azure AD: Offers Advanced recovery protections, including token expiration
- Duo Security: Supports multi-factor recovery verification with Audit logging

**Addresses:** [Broken Authentication](threat-details.md#broken-authentication)

## Secure Credential Storage and Removal of Hardcoded Secrets

*Preventive*

Eliminate hardcoded credentials and store all user credentials, API keys, and tokens exclusively in platform-secure storage (Keychain, Secure Enclave, Android Keystore) with strict access controls, ensuring no secrets reside in source code, configuration files, or unencrypted local storage.

**Addresses:** [M1: Improper Credential Usage](threat-details.md#m1-improper-credential-usage)

## Secure Handling and Minimal Exposure of StoreKit Artifacts

*Preventive*

Store receipts, transaction IDs, and StoreKit tokens only in secure platform storage (Keychain / Secure Enclave) and avoid caching or transmitting unvalidated purchase artifacts, reducing the risk of tampering, replay, or misuse of in-app purchase data.

**Addresses:** [Misuse of StoreKit or App Store APIs](threat-details.md#misuse-of-storekit-or-app-store-apis)

## Secure Service Token Management

*Preventive*

Implement secure generation, distribution, and storage protocols for service tokens used by Non-Person Entities. Ensure tokens are generated with strong cryptographic methods, distributed through secure channels, and stored in a protected environment to prevent unauthorized access and session hijacking.

**How to implement:**

- Use short-lived tokens to limit the window of opportunity for an attacker.
- implement token revocation mechanisms to invalidate Compromised tokens immediately.
- Employ secure Transport protocols (e.g., TLS) for token transmission.
- regularly Rotate tokens and keys to enhance security.
- Monitor and Log token usage for anomaly detection.
- Apply strict access controls to token storage locations.
- Use multi-factor authentication to further secure token access.

**Why it works:** Tokens are generated using strong cryptographic algorithms, ensuring randomness and unpredictability. TSecure token handling reduces the risk of interception, misuse, or privilege escalation. Enforcing strict token lifecycles, transmission protections, and anomaly detection enhances resilience against session hijacking and unauthorized access.

**Examples:**

- Examples of technology that implement secure service token management include:
- OAuth 2.0 for authorization, which uses access tokens with expiration times
- JSON Web Tokens (JWT) for secure token generation and transmission
- AWS Security Token Service (STS) for temporary security credentials. Tools like HashiCorp Vault for secure storage and management of tokens, and API gateways that enforce token validation and revocation policies are also relevant.

**Addresses:** [Session Hijacking](threat-details.md#session-hijacking)

## Secure Storage and Redaction of Purchase Artifacts

*Preventive*

Store App Store tokens, transaction IDs, and purchase receipts only in platform-secure storage (Keychain, Secure Enclave, encrypted keystore) and never in logs, UserDefaults, or flat files, ensuring sensitive purchase artifacts are encrypted at rest and inaccessible to other apps or local attackers.

**Addresses:** [Insecure Handling of App Store Purchase Tokens](threat-details.md#insecure-handling-of-app-store-purchase-tokens)

## Server-Side Receipt Validation and Secure StoreKit Workflows

*Preventive*

Perform transaction and receipt validation on a trusted backend using App Store–verified APIs, ensuring StoreKit data is never trusted solely from the client and preventing attackers from bypassing or forging purchase flows within the app.

**Addresses:** [Misuse of StoreKit or App Store APIs](threat-details.md#misuse-of-storekit-or-app-store-apis)

## Server-Side Receipt Validation With Trusted App Store Endpoints

*Preventive*

Validate all App Store receipts on a secure backend using Apple’s official verification APIs and cryptographic signatures, ensuring the client never directly authorizes purchases and preventing forged or tampered receipts from unlocking premium content.

**Addresses:** [Receipt Forgery and Validation Attacks](threat-details.md#receipt-forgery-and-validation-attacks)

## Server-Side Validation and Token Minimization

*Preventive*

Validate receipts and purchase tokens on a backend service instead of the client, and only cache short-lived, non-sensitive references on-device, reducing the exposure window and limiting the value of any locally compromised purchase data.

**Addresses:** [Insecure Handling of App Store Purchase Tokens](threat-details.md#insecure-handling-of-app-store-purchase-tokens)

## Signed Releases and Store-Only Distribution Controls

*Preventive*

Distribute mobile apps only through official, signed channels (App Store, Play Store, managed MDM) and enforce code-signing, certificate pinning, and build provenance checks so users and devices can verify that installed binaries originate from authorized store releases.

**Addresses:** [App Tampering or Fake Distribution Channels](threat-details.md#app-tampering-or-fake-distribution-channels)

## Source trusted libraries and packages

*Preventive*

Source components exclusively from official repositories. Regularly audit and update libraries and frameworks to ensure they are maintained and free from vulnerabilities.

**How to implement:**

- verify the integrity of libraries using checksums or digital signatures
- Use official repositories with active community and vendor support
- Monitor Security advisories for components in Use - automate Dependency Management and update tracking
- Establish a process for deprecating and replacing outdated libraries - limit or Review Use of third-party libraries from unknown or unverified sources

**Why it works:** Implement tools that source libraries from trusted repositories and verify integrity using digital signatures or checksums. Regular audits should identify outdated or risky components. Automate alerts for security advisories and enforce policies for deprecating unsupported libraries. Dependency managers help track third-party usage and reduce reliance on unverified sources, promoting safe and reliable software composition.

**Examples:**

- npm: sources packages from the official Node Registry and includes Audit tools
- Maven: manages Java dependencies from Maven Central with version control
- Composer: Pulls PHP libraries from Packagist and includes Security advisories
- GitHub Dependabot: Automates updates and Flags vulnerable packages
- Snyk: Scans Open-source libraries and recommends secure alternatives
- JFrog Artifactory: Hosts trusted internal and third-party components securely

**Addresses:** [Vulnerable and Outdated Components](threat-details.md#vulnerable-and-outdated-components)

## Strict Authorization Enforcement with Server-Side Access Controls

*Preventive*

Implement consistent server-side authorization checks for every API call, validating user roles, scopes, and resource ownership on the backend rather than the client, preventing privilege escalation, bypassing of role rules, or manipulation of client-side authorization logic.

**Addresses:** [M3: Insecure Authentication / Authorization](threat-details.md#m3-insecure-authentication--authorization)

## Strong Credential Handling, Rotation, and Least-Privilege Access

*Preventive*

Use short-lived, scoped tokens instead of static credentials, rotate secrets regularly, and apply least-privilege permissions on all keys and tokens to limit exposure if compromised, while enforcing secure handling practices such as TLS pinning, encrypted transport, and avoiding logging or debugging sensitive values.

**Addresses:** [M1: Improper Credential Usage](threat-details.md#m1-improper-credential-usage)

## Use safe APIs

*Preventive*

Use safe APIs that eliminate direct interpreter use. Emphasize structured interfaces (e.g., parameterized queries or secure libraries) to isolate user inputs from logic execution and minimize injection risks.

**How to implement:**

- Use parameterized queries or prepared statements instead of dynamic SQL.
- conduct Security-focused code reviews for API usage.
- Remove insecure legacy APIs that fail to sanitize inputs.
- Train developers on API misuse risks and secure interaction patterns.

**Why it works:** Safe APIs prevent injection by enforcing a clear separation between data and execution logic. These APIs reduce developer exposure to unsafe constructs. Code reviews and deprecation of unsafe interfaces ensure ongoing resilience.

**Examples:**

- Java JDBC: Prepared statements separate SQL logic from inputs.
- .NET Web APIs: Use input validation middleware for structured data handling.
- Google Cloud APIs: Enforce secure interface patterns through standardized request schemas.

**Addresses:** [Injection flaws](threat-details.md#injection-flaws)

## Use Trusted Frameworks

*Preventive*

Utilize established frameworks that ensure robust input validation, output encoding, and comprehensive authentication and authorization mechanisms.

**How to implement:**

- Choose frameworks with a strong Security track record and active community support.
- regularly update frameworks to incorporate Security patches.
- conduct Security assessments of the framework before implementation.
- ensure the framework Supports secure coding practices and guidelines.
- Validate third-party libraries for known vulnerabilities and compatibility.
- Provide training for developers on secure framework usage and best practices.

**Why it works:** Implementing trusted frameworks involves selecting established libraries that inherently support secure coding practices. These frameworks enforce input validation by sanitizing user inputs and applying output encoding to prevent XSS. They provide built-in authentication and authorization mechanisms, ensuring that users are correctly identified and authorized for actions. Regular updates and community support enhance security, while logging and monitoring help detect potential threats.

**Examples:**

- Examples of trusted frameworks:
- OWASP ESAPI (Enterprise Security API): Provides a set of APIs for secure input validation, output encoding, and authentication.
- Spring Security: A powerful framework for authentication and authorization in Java applications.
- Django: A Python web framework that includes built-in protections against XSS and CSRF.
- ASP.NET Core Identity: Offers comprehensive authentication and authorization features for .NET applications.

**Addresses:** [Improper authentication](threat-details.md#improper-authentication); [Information Disclosure](threat-details.md#information-disclosure); [Missing authentication](threat-details.md#missing-authentication); [Spoofing](threat-details.md#spoofing); [Weak Server-Side Controls](threat-details.md#weak-server-side-controls)

## Validate User Input

*Preventive*

Implement strict input validation to ensure user-provided data adheres to expected formats, types, and constraints. Reject or sanitize any input that does not meet these criteria to prevent potential security vulnerabilities such as injection attacks or unauthorized access.

**How to implement:**

- Use whitelisting for acceptable input formats and values.
- implement regular expressions to Enforce input patterns.
- limit input length to mitigate buffer overflow risks.
- Validate data types explicitly
- Employ context-aware encoding for output. -Add rate limiting to block brute-force input
- Use Security libraries or frameworks with built-in validation.
- Log and Monitor invalid input for analysis.

**Why it works:** Input validation ensures user data is clean, expected, and secure before processing. Strong validation prevents injection, overflow, and brute-force attacks. Input rules should align with business logic, and validation must happen both client- and server-side. Monitoring rejected inputs can help identify attack patterns and improve defenses over time.

**Examples:**

- Joi (Node.js): Define and enforce input schemas using clear syntax
- Validator.js: Validate and sanitize strings (e.g., emails, URLs)
- Express-validator: Middleware for input validation in Express apps
- Yup (JavaScript/TypeScript): Schema validation for form inputs
- OWASP ESAPI: Java library for input validation and encoding

**Addresses:** [Client-Side Injection](threat-details.md#client-side-injection); [Injection flaws](threat-details.md#injection-flaws); [Insecure Inter-Process Communication (IPC)](threat-details.md#insecure-inter-process-communication-ipc); [M4: Insufficient Input / Output Validation](threat-details.md#m4-insufficient-input--output-validation); [Weak Server-Side Controls](threat-details.md#weak-server-side-controls)

## Vetted, Pinned, and Continuously Monitored Dependencies

*Preventive*

Allow only approved third-party libraries, SDKs, and build tools that pass security review, pin versions to prevent unauthorized updates, and continuously monitor for CVEs or integrity changes using SCA/SBOM tooling to reduce the risk of introducing vulnerable or tampered components into the mobile app.

**Addresses:** [M2: Inadequate Supply Chain Security](threat-details.md#m2-inadequate-supply-chain-security)
