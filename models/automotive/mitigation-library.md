# Automotive: Mitigation Library

74 distinct mitigations, listed once each in alphabetical order, with the threats each one addresses. Back to the [threat details](threat-details.md) or the [model overview](README.md).

Control categories: **Preventive** stops an attack, **Detective** spots one in progress, **Corrective** limits damage and restores service.

## Access-Controlled Diagnostic Modes With Strong Authentication

*Preventive*

Restrict advanced UDS services (programming, memory access, configuration changes) to authenticated dealer tools or authorized service equipment, using secure challenge–response protocols and PINs/keys so attackers cannot invoke privileged diagnostic functions through OBD-II or remote gateways.

**Addresses:** [Diagnostic interface exploitation (OBD-II, UDS)](threat-details.md#diagnostic-interface-exploitation-obd-ii-uds)

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

**Addresses:** [Reverse Engineering](threat-details.md#reverse-engineering)

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

## Controlled USB / Wireless Interfaces With Policy Enforcement and Threat Detection

*Preventive*

Restrict Android Auto / CarPlay interfaces to approved protocols and validated message types, apply strict filtering at the USB/wireless ingress point, and monitor for anomalous behavior from connected devices to prevent malware or tampered apps from abusing integration channels to reach in-vehicle networks.

**Addresses:** [Compromised mobile app integrations (Android Auto / CarPlay)](threat-details.md#compromised-mobile-app-integrations-android-auto--carplay)

## Cryptographically Signed Firmware and Secure Boot Enforcement

*Preventive*

Require all ECU firmware and OTA packages to be cryptographically signed by a trusted OEM key, verify signatures and version metadata before any update is applied, and enforce secure boot so only verified firmware images can execute, blocking unauthorized or tampered reflashes.

**Addresses:** [ECU firmware manipulation or reflashing](threat-details.md#ecu-firmware-manipulation-or-reflashing)

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

## ECU Identity Verification With Message Authentication and Secure Gateways

*Preventive*

Require all CAN traffic to pass through a secure gateway that enforces message authentication (MACs, digital signatures, or link-layer authentication where supported) and validates sender identity against an authorized ECU list, ensuring forged or spoofed devices cannot masquerade as legitimate modules.

**Addresses:** [ECU impersonation / spoofing](threat-details.md#ecu-impersonation--spoofing)

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

**Addresses:** [Cryptographic failure](threat-details.md#cryptographic-failure); [Insecure Communication with Third-Party Services](threat-details.md#insecure-communication-with-third-party-services); [Insufficient Transport Layer Protection](threat-details.md#insufficient-transport-layer-protection)

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

**Addresses:** [Cryptographic failure](threat-details.md#cryptographic-failure); [Data Disclosure](threat-details.md#data-disclosure); [Insecure Data Storage](threat-details.md#insecure-data-storage); [Session Hijacking](threat-details.md#session-hijacking)

## End-to-End Signed OTA Packages With Secure Boot Enforcement

*Preventive*

Require all OTA update packages to be cryptographically signed by OEM-trusted keys and validated on-device before installation, and pair this with secure boot so only verified firmware can execute, preventing attackers from injecting malicious or altered update images into the infotainment unit.

**Addresses:** [Hijacked OTA (Over-the-Air) update mechanisms](threat-details.md#hijacked-ota-over-the-air-update-mechanisms)

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

## Engine Safety Limiters Enforced at Hardware and ECU Levels

*Corrective*

Implement hardware-level rev-limiters, temperature cutoffs, and fail-safe operating modes that cannot be overridden by CAN messages, ensuring protective shutdown systems remain functional even if the ECU is saturated or receiving malicious inputs.

**Addresses:** [Engine & Powertrain ECU Overload / Destructive DoS](threat-details.md#engine--powertrain-ecu-overload--destructive-dos)

## Fail-Safe ADAS Modes With Redundant Perception Paths

*Corrective*

Provide redundant sensing (camera + radar + ultrasonic), enforce safe fallback behavior when perception degrades (e.g., disengage ACC, limit steering assistance), and isolate ADAS ECUs from untrusted network domains, ensuring assistance systems fail safely instead of applying unsafe control actions.

**Addresses:** [ADAS Sensor Manipulation / Assistance System Degradation](threat-details.md#adas-sensor-manipulation--assistance-system-degradation)

## Gateway-Level Filtering and Segmentation of Diagnostic Traffic

*Preventive*

Route all diagnostic requests through a secure, policy-enforcing gateway ECU that filters UDS/OBD-II commands, blocks high-risk services by default, and isolates telematics or infotainment domains from the internal vehicle networks, preventing remote or unauthorized diagnostic access from reaching critical ECUs.

**Addresses:** [Diagnostic interface exploitation (OBD-II, UDS)](threat-details.md#diagnostic-interface-exploitation-obd-ii-uds)

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

## Hardened Bluetooth Pairing and Authenticated Sessions

*Preventive*

Enforce secure pairing modes (Just Works disabled where possible, prefer passkey/Numeric Comparison), require user interaction for new pairings, and bind Bluetooth sessions to authenticated, trusted device identities to prevent impersonation, unauthorized pairing, and eavesdropping on in-vehicle communications.

**Addresses:** [Bluetooth exploitation](threat-details.md#bluetooth-exploitation)

## Hardened Gateway ECUs With Domain Isolation and Message Authentication

*Preventive*

Implement strict domain isolation within the central gateway and enforce message authentication, ID filtering, and policy-based routing so even if a non-critical domain is compromised, malicious traffic cannot be bridged or forwarded into safety-critical CAN segments.

**Addresses:** [Gateway or bridge compromise](threat-details.md#gateway-or-bridge-compromise)

## Hardened OTA Delivery Infrastructure With Authenticated Update Channels

*Preventive*

Protect OTA servers, APIs, and distribution pipelines using strong authentication, encrypted channels, role-based access, and continuous integrity monitoring, ensuring attackers cannot compromise backend systems or spoof update sources to push unauthorized or persistent malware to vehicles.

**Addresses:** [Hijacked OTA (Over-the-Air) update mechanisms](threat-details.md#hijacked-ota-over-the-air-update-mechanisms)

## Hardened Update and Diagnostic Access Controls

*Preventive*

Restrict access to diagnostic ports and OTA update interfaces with strong authentication, role-based permissions, and locked-down reprogramming modes, and log all reflashing events, preventing untrusted tools or actors from initiating firmware updates outside approved service and OEM processes.

**Addresses:** [ECU firmware manipulation or reflashing](threat-details.md#ecu-firmware-manipulation-or-reflashing)

## Hardening of Infotainment OS and Isolation From Critical Networks

*Preventive*

Reduce the attack surface of infotainment systems through OS hardening (service minimization, sandboxing, memory protections, privilege separation) and isolate them from safety-critical networks using secure gateways, preventing a compromised infotainment OS from executing arbitrary code that could pivot deeper into the vehicle.

**Addresses:** [Exploiting unpatched software vulnerabilities](threat-details.md#exploiting-unpatched-software-vulnerabilities)

## Hardware-Backed Secure Key Storage and Non-Extractable Secrets

*Preventive*

Store all cryptographic keys, authentication tokens, and ECU credentials in hardware-backed secure elements or TPM-like modules, ensuring secrets are non-exportable, encrypted at rest, and never exposed directly in flash or RAM where chip-off or debug extraction attacks are possible.

**Addresses:** [Key or credential leakage from ECUs](threat-details.md#key-or-credential-leakage-from-ecus)

## Hardware-Enforced Safety Overrides and Fail-Safe Operating Modes

*Corrective*

Implement hardware-level safety systems (independent brake actuators, backup crash sensors, and non-bypassable airbag initiation circuits) that continue functioning even if the CAN bus is compromised, ensuring braking and airbag activation cannot be disabled via network commands.

**Addresses:** [Braking & Safety ECU Command Suppression / Safety System Disablement](threat-details.md#braking--safety-ecu-command-suppression--safety-system-disablement)

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

**Addresses:** [Broken access control](threat-details.md#broken-access-control); [Data Disclosure](threat-details.md#data-disclosure); [Weak Server-Side Controls](threat-details.md#weak-server-side-controls)

## Implement access control mechanisms

*Preventive*

Implement access control mechanisms consistently across the application to ensure that every user action is explicitly authorized. Validate permissions at all entry points, including API endpoints, services, and internal functions, to prevent unauthorized access to data and functionality.

**How to implement:**

- Define and document a unified access control strategy for all system components.
- Enforce access control at multiple layers (API gateway, backend services, databases).
- Use centralized policy engines (e.g., RBAC or ABAC) to apply consistent rules.
- Perform static and dynamic testing to identify endpoints lacking access checks.
- Monitor access patterns and log unauthorized attempts for analysis.
- Train developers to apply consistent authorization checks during development.

**Why it works:** Consistent access control ensures that no part of the application allows unauthorized access due to missing or inconsistent permission checks. Implementing centralized enforcement mechanisms like RBAC or ABAC ensures rules are uniformly applied across all endpoints and services. Security tools should verify that access control policies are in place at every interaction point. Logging, audits, and testing tools help maintain coverage and identify violations over time.

**Examples:**

- AWS IAM for managing user permissions and roles.
- OAuth 2.0 for delegated access control in APIs, ensuring users can only access resources they are authorized to.
- API Gateway services (e.g., Amazon API Gateway, Azure API Management) that enforce access policies at the function level.
- Open Policy Agent (OPA) for implementing fine-grained access control based on policies.
- Role-based access control features in platforms like Microsoft Azure Active Directory.

**Addresses:** [Broken access control](threat-details.md#broken-access-control)

## Implement an anonymity system

*Preventive*

Implement an anonymity system that obscures users' identities and personal data during digital interactions. Ensure that no identifiable information, such as location or user actions, is exposed. Utilize tools and methods that prevent linking, identifying, and detecting threats, thereby minimizing data disclosure risks.

**How to implement:**

- Avoid collecting PII such as IP addresses and location data
- Replace persistent identifiers with rotating session tokens
- Use mix networks, onion routing, or VPNs to obscure source IPs
- Apply data minimization principles, only collect what's strictly necessary
- Remove or obfuscate metadata from transmitted content
- Conduct regular privacy audits to identify and mitigate potential tracking vectors
- Educate users and developers about fingerprinting risks and how to reduce traceability

**Why it works:** The anonymity system hides user identities by avoiding persistent identifiers, masking network-level metadata, and rotating session data. It limits data collection, uses encryption, and avoids storing identifiable information. These measures prevent profiling and tracking during digital interactions.

**Examples:**

- Tor: Enables anonymous Web access.
- signal: Encrypts messages and hides metadata.
- VPNs: mask IP and location data.
- ARX: Anonymizes structured datasets.
- Tails OS: Preserves anonymity by design.

**Addresses:** [Data Disclosure](threat-details.md#data-disclosure)

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

## Implement privacy-preserving authentication methods.

*Preventive*

Implement privacy-preserving authentication methods that verify user or device identities while minimizing personal information disclosure. Use techniques that ensure secure and reliable authentication without compromising user privacy. Focus on reducing the amount of sensitive data collected and shared during the authentication process.

**How to implement:**

- Utilize zero-knowledge proofs to authenticate users without revealing sensitive Information - implement multi-factor authentication that relies on less intrusive data sources
- Use temporary or Session-based identifiers instead of persistent identifiers - regularly Audit authentication logs to minimize data retention and exposure - ensure that authentication systems are Designed to limit data sharing to necessary parties Only, Avoid centralized storage of authentication data where possible

**Why it works:** Key characteristics of privacy-preserving authentication include limiting data disclosure, supporting anonymous or pseudonymous access, using secure encryption, and decentralization. Techniques like zero-knowledge proofs allow validation without revealing sensitive information. These methods reduce privacy risks in sensitive contexts such as banking or digital identity verification.

**Examples:**

- ZK-SNARKs (Zero-Knowledge Succinct Non-Interactive Arguments of Knowledge) for blockchain transactions.
- FIDO2/WebAuthn for passwordless authentication.
- Privacy-focused identity providers like uPort or Sovrin.
- Temporary session tokens in OAuth 2.0.
- Decentralized authentication tools that do not require user registration with a central server.

**Addresses:** [Data Disclosure](threat-details.md#data-disclosure)

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

**Addresses:** [Data Disclosure](threat-details.md#data-disclosure)

## Implement Private Information Retrieval (PIR) techniques.

*Preventive*

Implement PIR techniques that allow users to retrieve specific data from databases without revealing which items are accessed. Ensure the process protects query privacy, uses secure server models, and supports efficiency and scalability in sensitive systems.

**How to implement:**

- ensure PIR implementations Maintain query privacy under both single- and multi-server models.
- Choose between computational or Information-theoretic PIR based on system constraints.
- evaluate performance trade-offs, especially for large-scale databases.
- Apply PIR in scenarios requiring query confidentiality, such as cloud or library access.
- Monitor usage patterns and Log performance for optimization and anomaly detection.

**Why it works:** PIR techniques enable users to retrieve data without disclosing their query to the server. Systems may use computational PIR (based on mathematical hardness assumptions) or information-theoretic PIR (relying on multiple non-colluding servers). These techniques preserve privacy while balancing performance, with trade-offs in efficiency and scalability depending on the implementation.

**Examples:**

- Oblivious Transfer protocols: used in systems that allow data Retrieval without query exposure.
- multi-server PIR frameworks: like Sharemind and Enigma, where no single server knows the full query.
- Homomorphic encryption-based PIR: Microsoft SEAL or IBM HELib allow computation on encrypted data.
- cloud file Retrieval systems: Let users access specific files without revealing file interests.

**Addresses:** [Data Disclosure](threat-details.md#data-disclosure)

## Implement pseudonymity systems

*Preventive*

Implement pseudonymity systems to enable users to perform activities under a pseudonym, safeguarding their real identities. Ensure that the system maintains accountability for actions taken under these pseudonyms while preventing direct identification. Regularly assess and minimize data collection, processing, and sharing to align with the principle of data minimization.

**How to implement:**

- Use distinct pseudonyms for different contexts to prevent cross-linking.
- ensure pseudonym systems support traceability for accountability where legally required.
- combine pseudonymity with PETs like encryption and anonymous communications.
- Design with legal and ethical boundaries in mind to prevent misuse or profiling.

**Why it works:** Pseudonymity systems let users act without revealing real identities, supporting privacy and trusted interactions. By assigning distinct pseudonyms across contexts, they prevent linkability. When paired with PETs, they enhance confidentiality. Design must support accountability when needed and avoid misuse, profiling, or legal violations.

**Examples:**

- Use UUIDs or hash functions to generate pseudonymous user IDs.
- Integrate tools like SimpleLogin for pseudonymous email addresses.
- Apply consistent pseudonyms using salted hashes across sessions.
- combine with encryption libraries (e.g., libsodium) to prevent linkability.
- Use Tor hidden services for pseudonymous Service hosting.

**Addresses:** [Data Disclosure](threat-details.md#data-disclosure)

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

**Addresses:** [Broken Authentication](threat-details.md#broken-authentication); [Session Hijacking](threat-details.md#session-hijacking)

## Implement Timely Patching

*Preventive*

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

## Input Validation and Gateway-Level Sanitization of Network Traffic

*Preventive*

Validate all inbound CAN, UDS, and diagnostic payloads at a secure gateway ECU, enforcing protocol correctness, length limits, and service-level restrictions so malformed or oversized packets never reach vulnerable modules, reducing exploitation opportunities against high-privilege ECU firmware.

**Addresses:** [Memory corruption or buffer overflow in ECU software](threat-details.md#memory-corruption-or-buffer-overflow-in-ecu-software)

## Locked-Down Bootloader Access and Controlled Update Paths

*Preventive*

Disable or restrict bootloader reprogramming interfaces, require authenticated flashing sessions through approved service tools, and log or alert on any bootloader access attempts, ensuring attackers cannot exploit open or poorly protected boot modes to install persistent malicious firmware.

**Addresses:** [Exploiting insecure bootloaders](threat-details.md#exploiting-insecure-bootloaders)

## Locked-Down Debug/Programming Interfaces With Secure Access Controls

*Preventive*

Disable or tightly restrict JTAG, SWD, and other debug/programming interfaces on production ECUs, require authenticated and authorized service sessions for any access, and log all attempts, preventing attackers from extracting keys or internal secrets through physical probing or low-level diagnostic channels.

**Addresses:** [Key or credential leakage from ECUs](threat-details.md#key-or-credential-leakage-from-ecus)

## Mandatory Firmware Lifecycle Management and Decommissioning

*Preventive*

Establish strict firmware lifecycle policies that require OEMs to maintain security updates for supported model years and explicitly decommission or block unsupported firmware from operating, ensuring outdated infotainment systems cannot remain in use with known exploitable vulnerabilities.

**Addresses:** [Exploiting legacy or unsupported firmware](threat-details.md#exploiting-legacy-or-unsupported-firmware)

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

## Memory-Safe Parsing, Bounds Enforcement, and Hardened Firmware Builds

*Preventive*

Use strict bounds checking, validated parsing routines, and safe memory-handling patterns in ECU firmware, combined with compiler hardening features (stack canaries, ASLR, DEP, and fortified libc) to prevent malformed CAN or diagnostic packets from triggering memory corruption or enabling arbitrary code execution.

**Addresses:** [Memory corruption or buffer overflow in ECU software](threat-details.md#memory-corruption-or-buffer-overflow-in-ecu-software)

## Message Freshness Enforcement With Counters, Nonces, or Timestamps

*Preventive*

Introduce freshness checks at the secure gateway or ECU level—such as rolling counters, monotonic timestamps, or nonce-based challenges—so each CAN message is validated as “new” and any replayed or out-of-sequence frames are rejected before reaching critical modules.

**Addresses:** [Replay attacks on CAN traffic](threat-details.md#replay-attacks-on-can-traffic)

## Privacy-Respecting Voice Processing and Restricted Data Exposure

*Preventive*

Minimize voice data sent to third-party servers by preferring on-device processing where possible, encrypt all transmitted audio, and restrict the assistant’s access to contacts, messages, and vehicle/system controls to least-privilege scopes, reducing both command-abuse impact and privacy leakage if voice traffic is intercepted or misused.

**Addresses:** [Voice-assistant command injection](threat-details.md#voice-assistant-command-injection)

## Rate-Limited, Authenticated Control Traffic Through a Secure Gateway

*Preventive*

Enforce message authentication, CAN ID whitelisting, and strict rate limits at the central secure gateway to prevent attackers from flooding the Engine ECU with spoofed or excessive control commands, ensuring the ECU cannot be overwhelmed into unsafe operating states.

**Addresses:** [Engine & Powertrain ECU Overload / Destructive DoS](threat-details.md#engine--powertrain-ecu-overload--destructive-dos)

## Rate-Limiting and Priority Enforcement at Secure Gateways

*Preventive*

Use a secure gateway ECU to enforce per-ID rate limits, validate arbitration priority usage, and drop frames that exceed allowable transmission frequency so attackers cannot monopolize CAN bandwidth or suppress legitimate safety-critical traffic.

**Addresses:** [Bus flooding / Denial-of-service (DoS)](threat-details.md#bus-flooding--denial-of-service-dos)

## Regular, Secure, and Verified Software Update Pipelines

*Preventive*

Implement a robust OTA and service-update process that delivers timely security patches, verifies update integrity with digital signatures, and ensures all infotainment components—including third-party OS modules—receive consistent, OEM-controlled updates to eliminate known vulnerabilities before attackers can exploit them.

**Addresses:** [Exploiting unpatched software vulnerabilities](threat-details.md#exploiting-unpatched-software-vulnerabilities)

## Restricted Bluetooth Attack Surface and Anomaly-Aware Handling

*Preventive*

Limit Bluetooth-exposed services and commands to the minimum required, validate all inbound messages for format and authorization, and implement rate limiting and timeout handling so malformed packets, repeated pairing attempts, or unexpected commands cannot access internal data paths or trigger denial-of-service conditions.

**Addresses:** [Bluetooth exploitation](threat-details.md#bluetooth-exploitation)

## Restricted USB Functionality With Strict Parsing and Allowed Device Profiles

*Preventive*

Limit USB interfaces to approved device classes (media-only, charging-only, no HID/emulation) and enforce hardened parsing for file systems and media formats, ensuring malformed or crafted USB content cannot trigger parser vulnerabilities or arbitrary code execution in infotainment or diagnostic components.

**Addresses:** [Malicious USB device injection](threat-details.md#malicious-usb-device-injection)

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

## Secure Gateway Enforcement With Anomaly Detection and Access Controls

*Detective*

Use a hardened central gateway that authenticates cross-domain traffic, blocks unauthorized service requests, and monitors for abnormal message patterns or attempted domain escalation, preventing compromised infotainment components from sending or relaying commands to vehicle-control networks.

**Addresses:** [Lateral movement to CAN or vehicle control networks](threat-details.md#lateral-movement-to-can-or-vehicle-control-networks)

## Secure Gateway Filtering With Context and Rate Validation

*Preventive*

Route CAN traffic through a secure gateway that enforces contextual validation (expected timing, message frequency, and ECU state), blocking messages that repeat too quickly or appear outside their normal operational window, preventing attackers from replaying captured commands like unlock or start signals.

**Addresses:** [Replay attacks on CAN traffic](threat-details.md#replay-attacks-on-can-traffic)

## Secure Gateway Filtering With Safety-Critical Message Authentication

*Preventive*

Route all braking and safety-related CAN traffic through a hardened secure gateway that enforces message authentication, ID whitelisting, and rate limits, blocking spoofed or manipulated frames from suppressing brake commands or disabling airbag deployment logic.

**Addresses:** [Braking & Safety ECU Command Suppression / Safety System Disablement](threat-details.md#braking--safety-ecu-command-suppression--safety-system-disablement)

## Secure Gateway Firmware, Access Controls, and Continuous Monitoring

*Detective*

Protect the gateway ECU with signed firmware, locked-down diagnostic/update interfaces, and runtime monitoring of cross-domain traffic patterns, immediately blocking or alerting on anomalous bridging behaviors that could indicate compromise or lateral movement from infotainment or telematics systems.

**Addresses:** [Gateway or bridge compromise](threat-details.md#gateway-or-bridge-compromise)

## Secure Gateway Isolation and Hardening of Legacy Components

*Preventive*

Isolate legacy or unpatched infotainment modules behind a secure gateway with restricted privileges, service minimization, and strict traffic filtering, preventing known-vulnerable components from reaching safety-critical networks or exposing exploitable surfaces to remote attackers.

**Addresses:** [Exploiting legacy or unsupported firmware](threat-details.md#exploiting-legacy-or-unsupported-firmware)

## Secure Gateways With Message Authentication and Signal Validation

*Preventive*

Route all CAN traffic through a secure gateway ECU that enforces message-level authentication, verifies signal plausibility, and blocks packets from untrusted sources, ensuring forged or out-of-context CAN frames cannot reach safety-critical modules or control surfaces.

**Addresses:** [Unauthorized CAN message injection](threat-details.md#unauthorized-can-message-injection)

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

## Segmented CAN Networks With DoS-Resilient Isolation

*Preventive*

Isolate safety-critical ECUs on protected CAN segments and use bus guardians or hardware firewalls to block excessive or malformed traffic from non-critical domains, ensuring essential control and sensor messages continue to flow even during a flooding attempt.

**Addresses:** [Bus flooding / Denial-of-service (DoS)](threat-details.md#bus-flooding--denial-of-service-dos)

## Segmented CAN Networks With Strict ECU Access Controls

*Preventive*

Isolate safety-critical ECUs on protected CAN segments and restrict write permissions to authorized modules only, using firewalling, ID filtering, and rate-limiting at the network layer to prevent unauthorized devices from injecting commands or flooding bus traffic.

**Addresses:** [Unauthorized CAN message injection](threat-details.md#unauthorized-can-message-injection)

## Segmented Network Architecture With ECU Whitelisting and ID Filtering

*Preventive*

Isolate critical ECUs on protected CAN segments and enforce strict ID filtering and ECU whitelisting so only approved modules can transmit on specific message IDs or bus zones, preventing malicious devices from injecting spoofed control frames or responding on behalf of trusted ECUs.

**Addresses:** [ECU impersonation / spoofing](threat-details.md#ecu-impersonation--spoofing)

## Sensor Fusion Validation and Secure ADAS Message Filtering

*Preventive*

Implement cross-sensor validation, plausibility checks, and CAN message filtering inside the ADAS ECU so spoofed or missing data (e.g., fake distance readings or lane markers) is detected and rejected, preventing manipulated sensor inputs from degrading lane-keeping or adaptive cruise control.

**Addresses:** [ADAS Sensor Manipulation / Assistance System Degradation](threat-details.md#adas-sensor-manipulation--assistance-system-degradation)

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

## Strict Isolation and Sandboxing Between Mobile and Infotainment Domains

*Preventive*

Enforce hardened isolation between Android Auto / CarPlay processes and the infotainment system, using sandboxing, containerization, and restricted IPC so connected mobile apps cannot access privileged interfaces or pivot into vehicle-side services, even if the phone is compromised.

**Addresses:** [Compromised mobile app integrations (Android Auto / CarPlay)](threat-details.md#compromised-mobile-app-integrations-android-auto--carplay)

## Strong Network Segmentation With Isolated Safety-Critical Domains

*Preventive*

Physically and logically isolate infotainment, telematics, and connectivity modules from safety-critical CAN networks, enforcing strict gateway policies, message filtering, and one-way dataflows so that a compromise in an internet-facing subsystem cannot propagate into braking, steering, or powertrain ECUs.

**Addresses:** [Lateral movement to CAN or vehicle control networks](threat-details.md#lateral-movement-to-can-or-vehicle-control-networks)

## USB Port Access Controls and Execution Barriers for Untrusted Devices

*Preventive*

Require user approval or service-mode authentication before enabling privileged USB operations (e.g., firmware loading or diagnostic access), and block automatic execution of scripts or update files, preventing malicious USB devices from bypassing network defenses to deliver payloads or manipulate ECU systems.

**Addresses:** [Malicious USB device injection](threat-details.md#malicious-usb-device-injection)

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

**Addresses:** [Weak Server-Side Controls](threat-details.md#weak-server-side-controls)

## User-Verified Actions and Robust Command Authentication

*Preventive*

Require explicit user verification (wake word, proximity checks, or confirmation prompts) for sensitive actions such as dialing, data access, and system changes, and harden the voice stack against ultrasonic/inaudible patterns by filtering inaudible frequencies and enforcing human-audible command characteristics.

**Addresses:** [Voice-assistant command injection](threat-details.md#voice-assistant-command-injection)

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

**Addresses:** [Client-Side Injection](threat-details.md#client-side-injection); [Insecure Inter-Process Communication (IPC)](threat-details.md#insecure-inter-process-communication-ipc); [Weak Server-Side Controls](threat-details.md#weak-server-side-controls)

## Verified Boot With Hardware-Backed Root of Trust

*Preventive*

Enforce secure boot on all ECUs by establishing a hardware-backed root of trust that validates firmware signatures, version metadata, and integrity before execution, preventing any unsigned or tampered boot images from loading—even after reboots or power cycles.

**Addresses:** [Exploiting insecure bootloaders](threat-details.md#exploiting-insecure-bootloaders)
