# LLM and Agentic Systems: Mitigation Library

142 distinct mitigations, listed once each in alphabetical order, with the threats each one addresses. Back to the [threat details](threat-details.md) or the [model overview](README.md).

Control categories: **Preventive** stops an attack, **Detective** spots one in progress, **Corrective** limits damage and restores service.

## Access-Controlled Embedding Exposure

*Preventive*

Restrict access to raw embeddings using strict authentication, least-privilege authorization, and service-to-service allowlists so only trusted internal components can retrieve or interact with vector data, preventing adversaries from obtaining embeddings for inversion attempts.

**Addresses:** [Embedding Inversion / Reconstruction](threat-details.md#embedding-inversion--reconstruction)

## Alert on skewed LLM responses

*Detective*

Implement monitoring to detect and alert when the number of skewed LLM responses surpasses a predefined threshold.

**How to implement:**

- Establish baseline metrics for normal response patterns to Identify anomalies.
- Utilize user feedback mechanisms to flag potentially skewed responses.
- implement regular audits of training data for integrity and accuracy.
- Develop a rapid response protocol for addressing flagged responses.
- incorporate diverse data sources to mitigate bias in training datasets.
- Train models with adversarial examples to enhance robustness against malicious inputs.

**Why it works:** The system monitors LLM responses in real time, comparing them against baseline metrics to detect skewed outputs. Anomaly detection triggers alerts when deviations exceed thresholds. User feedback helps refine accuracy. Regular audits and adversarial training improve robustness. Rapid response protocols are activated for flagged cases.

**Examples:**

- OpenAI's moderation tools that flag inappropriate or biased outputs from models.
- Google Cloud's AI and machine learning tools that include monitoring and anomaly detection features.
- IBM Watson's AI Fairness 360 toolkit, which helps identify and mitigate bias in AI models.
- Microsoft Azure's responsible AI dashboard that tracks model performance and fairness metrics.
- Amazon SageMaker’s built-in monitoring capabilities for detecting anomalies in model predictions.

**Addresses:** [Adversarial Examples](threat-details.md#adversarial-examples); [Data Poisoning - Training Phase](threat-details.md#data-poisoning---training-phase); [Malicious pre-training](threat-details.md#malicious-pre-training)

## Anomaly Detection and Segmentation of High-Sensitivity Vectors

*Detective*

Continuously monitor the index for abnormal clustering patterns and segregate high-sensitivity vectors into dedicated indexes or trust tiers with stricter write policies, blocking attacker-crafted vectors from co-locating with and hijacking similarity search around sensitive content.

**Addresses:** [Index Poisoning](threat-details.md#index-poisoning)

## Apply access and privilege management for AI agents

*Preventive*

Restrict AI agents to only the permissions and resources they need, minimizing damage if one is compromised.

**How to implement:**

- Enforce least privilege by default. over-permissioned agents increase attack surface. Define minimal access profiles and Enforce through IAM roles or Service accounts.
- Segregated Execution environments. Shared Execution can Enable lateral movement. isolate agents in containers, VMs, or dedicated namespaces to confine their reach.
- control access to sensitive APIs with approval gates. high-risk actions (e.g., data deletion) should Require explicit authorization. Add approval workflows, rate limits, or Policy-based controls.

**Why it works:** Restricting privileges limits the scope of damage if an agent is hijacked. By applying least privilege, sandboxing, and gated access to critical APIs, the ecosystem ensures that agents cannot overstep their intended boundaries or misuse resources.

**Examples:**

- Use Kubernetes namespaces with RBAC to sandbox agents, AWS IAM roles with least-privilege policies for resource access, and OPA policies to gate sensitive API calls.

**Addresses:** [Agent Identity Attack](threat-details.md#agent-identity-attack); [Agent Impersonation](threat-details.md#agent-impersonation); [Agent Tool Misuse](threat-details.md#agent-tool-misuse); [Compromised Agents](threat-details.md#compromised-agents); [Data Exfiltration](threat-details.md#data-exfiltration); [Framework Evasion](threat-details.md#framework-evasion); [Lateral Movement - AI infrastructure](threat-details.md#lateral-movement---ai-infrastructure); [Model Stealing](threat-details.md#model-stealing)

## Apply Fine-Grained Access Controls and Contextual Authorization for Metadata Exposure

*Preventive*

Apply fine-grained authorization that validates a requester’s permission to access both the underlying document and its associated metadata, blocking retrieval of structural or sensitive metadata by unprivileged users or agents.

**Addresses:** [Metadata leakage](threat-details.md#metadata-leakage)

## Architect distinct LLMs for specific use cases.

*Preventive*

Verify the specific use case for the LLM and its application. Develop distinct models by using separate training data or fine-tuning tailored to each use case. This approach enhances the accuracy and relevance of generative AI outputs for their intended purposes.

**How to implement:**

- clearly Define the distinct roles and tasks for each LLM to ensure optimal specialization.
- fine-Tune or Train each LLM on domain-specific datasets relevant to its role.
- Avoid overlapping functionalities to reduce redundancy and prevent conflicts between models.
- Maintain separation of access and data pathways between models to preserve performance and security.
- Periodically evaluate each LLM’s performance to adjust for evolving Use cases.

**Why it works:** Using distinct LLMs tailored to specific roles enhances task specialization, performance, and response accuracy. Each model focuses on a defined domain, reducing conflict and enabling more accurate, efficient outputs. Separation also improves security and makes it easier to scale and adapt to evolving use cases.

**Examples:**

- OpenAI fine-Tuning API: Tailors models for specific tasks
- Google Vertex AI: Custom training with access controls
- IBM Watson Studio: Tracks data lineage and provenance
- Microsoft Azure ML: Monitors and manages deployed models
- H2O.ai: audits training data for integrity verification

**Addresses:** [Inject malicious stuff into training process](threat-details.md#inject-malicious-stuff-into-training-process); [Malicious pre-training](threat-details.md#malicious-pre-training)

## Automate API documentation generation and restrict access to authorized users only

*Preventive*

Automate API documentation generation and restrict access to authorized users. Ensure all API versions are protected with external security measures to prevent unauthorized access. Regularly audit and update inventory to remove outdated or vulnerable endpoints.

**How to implement:**

- Use CI/CD tools to automate API documentation generation.
- Restrict access to documentation tools and outputs using RBAC.
- secure automated pipelines with authentication and access controls.
- regularly Review permissions for access to generated documentation.
- Validate that generated docs Do not expose internal or deprecated APIs.
- Maintain version control for API documentation.

**Why it works:** Automated API documentation is generated using CI/CD tools to ensure consistency and up-to-date information. Access to the documentation and generation process is restricted through role-based access control (RBAC). Permissions are reviewed regularly, and documentation is checked to ensure no internal or deprecated APIs are exposed.

**Examples:**

- Swagger & OpenAPI: generate docs from API code and Restrict access via CI/CD.
- Postman: Supports documentation versioning and access control.
- Azure API Management: Enforces access restrictions to API docs.
- AWS API gateway: Provides private doc endpoints with IAM controls.
- GitHub actions: Automates doc updates with role-based access.

**Addresses:** [Improper Inventory Management](threat-details.md#improper-inventory-management)

## Automate configuration assessments

*Detective*

Automate the evaluation of configurations and settings across all environments to identify vulnerabilities and ensure compliance with security standards.

**How to implement:**

- Schedule regular automated Scans to Identify outdated or insecure configurations.
- implement continuous monitoring to detect configuration drift.
- Integrate configuration assessments into CI/CD pipelines for early detection.
- Utilize centralized logging to track configuration changes and access attempts.
- Maintain an inventory of all configurations and their compliance status.

**Why it works:** Automated configuration assessments use tools to scan environments for compliance with security benchmarks. These tools pull configuration data, compare it against standards, and flag issues for remediation. Integration with CI/CD pipelines ensures new deployments are assessed early. Centralized logging supports audit trails and anomaly detection.

**Examples:**

- AWS config: Evaluates resource configs against best practices
- Terraform: Automates validation of infrastructure code
- Chef InSpec: tests configurations against Security controls
- OpenSCAP: checks systems against Security policies
- Qualys: Monitors misconfigurations and vulnerabilities in cloud

**Addresses:** [Orchestration Attacks](threat-details.md#orchestration-attacks); [Security Misconfiguration (API)](threat-details.md#security-misconfiguration-api)

## Block Non-Human Traffic

*Preventive*

Implement controls to detect and block non-human traffic, such as bots or automated tools, using behavioral analysis and known threat sources like Tor exit nodes and proxy IPs. Restrict unauthorized automation to protect sensitive business flows.

**How to implement:**

- Enforce rate limits to reduce abuse from high-frequency requests.
- trigger CAPTCHA challenges for suspicious or automated access.
- block or flag traffic from Tor nodes and Proxy IPs using threat intelligence feeds.
- Use device fingerprinting to Validate Session legitimacy.
- Monitor API usage patterns for automation and update detection rules regularly.

**Why it works:** The system detects non-human traffic by analyzing user behavior, such as unusual access frequency or patterns inconsistent with typical user interactions. Traffic from known Tor nodes or proxy services is blocked using threat intelligence feeds. Suspicious sessions are challenged with CAPTCHA, while device fingerprinting helps verify session legitimacy. Logging and analytics track anomalies and update detection mechanisms to improve resilience against automated threats.

**Examples:**

- Cloudflare Bot Management: uses machine learning to detect and block bots in Real time.
- Akamai Bot Manager: Analyzes behavior and Enforces access controls for automated requests.
- Google reCAPTCHA: challenges suspicious users to distinguish humans from bots.
- Distil networks: Provides Advanced Bot mitigation through traffic pattern analysis and threat feeds.
- PerimeterX Bot Defender: Offers API protection by detecting non-human behavior at scale.

**Addresses:** [Unrestricted Access to Sensitive Business Flows](threat-details.md#unrestricted-access-to-sensitive-business-flows)

## Catalog integrated services and their data handling

*Detective*

Create and maintain an up-to-date inventory of all integrated services, detailing their functions, data exchanged, and sensitivity levels. Regularly review and remove outdated API versions and unpatched endpoints. Ensure third-party services comply with security standards to prevent unauthorized access and data leaks.

**How to implement:**

- set a regular Schedule to update Service inventory.
- Use tools to track outdated APIs and endpoints.
- assess third-party services before integration.
- Define data handling rules by sensitivity level.
- Train staff on recognizing outdated services.
- Monitor for unauthorized access and vulnerabilities.

**Why it works:** A centralized inventory catalogs all integrated services, including data flow and sensitivity levels. Automated tools track outdated endpoints, and alerts prompt reviews. Manual checks verify third-party compliance. Staff receive training on inventory upkeep and risk awareness. This ensures integrations meet security standards.

**Examples:**

- API Management platforms like Apigee and AWS API gateway Offer features to track and manage API versions, ensuring outdated versions are identified and removed.
- Security tools such as Qualys or Nessus can scan for unpatched endpoints and vulnerabilities, providing alerts for remediation.
- third-party risk Management solutions like BitSight and SecurityScorecard assess the Security posture of integrated services before onboarding.

**Addresses:** [Improper Inventory Management](threat-details.md#improper-inventory-management)

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

**Addresses:** [Backdoor Attacks - AI framework](threat-details.md#backdoor-attacks---ai-framework); [Compromised Framework Components](threat-details.md#compromised-framework-components); [Supply Chain Attacks](threat-details.md#supply-chain-attacks); [Supply Chain Attacks - Cross-Layer](threat-details.md#supply-chain-attacks---cross-layer)

## Conduct targeted security testing for domain-specific risks

*Detective*

Developers must test AI agents against security risks specific to their industry or function, using targeted penetration testing, red teaming, and compliance-driven validation methods.

**How to implement:**

- Develop sector-specific test cases: Build test scenarios reflecting real-world attacks in the industry (e.g., medical data exfiltration in healthcare, fraudulent trading in finance).
- Apply red teaming techniques: Simulate adversaries that exploit workflows unique to the domain.
- Validate against compliance: checks Ensure testing also verifies adherence to standards like HIPAA, PCI DSS, or EU AI Act.

**Why it works:** Generic testing cannot catch all vertical vulnerabilities. Targeted testing ensures the agent can withstand realistic sector-specific attacks while proving compliance with regulatory and organizational requirements.

**Examples:**

- A healthcare AI agent is red-teamed with simulated prompt injections to extract PHI. Testing uses OWASP ZAP for API fuzzing, Guardrails.ai for LLM behavior validation, and custom red team scripts. Logs are monitored in Splunk to confirm PHI access is blocked and alerts trigger in line with HIPAA rules.

**Addresses:** [Evasion of Detection](threat-details.md#evasion-of-detection); [Horizontal/Vertical Solution Vulnerabilities](threat-details.md#horizontalvertical-solution-vulnerabilities); [Supply Chain Attacks - Cross-Layer](threat-details.md#supply-chain-attacks---cross-layer)

## Controlled Reindexing Pipelines with Source Validation

*Preventive*

Restrict reindexing to approved data sources and enforce validation checks (integrity, provenance, schema conformity) on all content before it enters the indexing pipeline, preventing unvetted or poisoned material from influencing the retrieval corpus.

**Addresses:** [Model Drift via Reindexing](threat-details.md#model-drift-via-reindexing)

## Defend AI models against sponge and resource-exhaustion inputs

*Preventive*

Protect AI models from denial-of-service conditions caused by adversarially crafted "sponge" inputs or oversized requests that consume excessive computational resources. This mitigation enforces input validation, resource quotas, and adversarial testing to prevent model-level DoS and ensure continued availability for dependent AI agents.

**How to implement:**

- Enforce maximum input size (e.g., token length, image dimensions, sequence depth) and truncate or reject inputs that exceed thresholds.
- Monitor inference FLOPs, memory allocation, and processing time per input. Flag anomalies such as inputs consuming significantly more resources than baseline.
- Apply per-user and per-session quotas for GPU time, memory usage, and concurrent queries. Terminate requests that exceed defined limits.
- Use adversarial detection filters to identify crafted inputs designed to maximize resource consumption.
- Redirect traffic to smaller, approximate, or cached models when thresholds are breached.
- Include sponge and oversized input scenarios in resilience testing campaigns.
- Route DoS/sponge alerts to SIEM/SOAR systems for automated containment (e.g., user throttling, IP blocking).

**Why it works:** Traditional DoS defenses focus on API or network flooding, but sponge attacks target the model itself with inputs that maximize computation time. Without input validation and resource quotas, attackers can starve GPU/CPU resources and cause service unavailability. By limiting input complexity, profiling resource usage, and testing models against adversarial inputs, organizations can defend against model-level DoS and maintain AI ecosystem reliability.

**Examples:**

- Input validation: Hugging Face 'transformers' max token parameters; TensorFlow input shape validation.
- Resource quotas: NVIDIA Triton Inference Server with per-request GPU limits; Kubernetes resource quotas.
- Monitoring: Prometheus/Grafana dashboards for GPU utilization anomalies; Datadog ML inference monitoring.
- Adversarial testing: IBM Adversarial Robustness Toolbox (ART) sponge attacks module; MITRE ATLAS adversarial DoS scenarios.

**Addresses:** [Denial of Service (DoS) Attacks - AI model](threat-details.md#denial-of-service-dos-attacks---ai-model)

## Defend framework APIs against distributed denial-of-service (DDoS) attacks

*Preventive*

Protect framework APIs from distributed denial-of-service attacks by using layered defenses including network-level protections, API-aware filtering, and resilient infrastructure design. Ensure framework services remain available and reliable under high-volume attack conditions.

**How to implement:**

- Deploy DDoS protection services (e.g., AWS Shield Advanced, Azure DDoS Protection, Google Cloud Armor, Cloudflare).
- Use Web Application Firewalls (WAFs) to block malicious traffic targeting API endpoints.
- Implement traffic scrubbing and rate-based filtering at the CDN or edge network level.
- Design APIs with elastic scaling and auto-healing to absorb sudden traffic surges.
- Employ behavioral analysis to distinguish legitimate requests from botnet floods.
- Ensure redundant API endpoints and failover mechanisms to maintain service availability.
- Correlate with monitoring and anomaly detection for early alerting. (Refer to 'Implement behavioral monitoring and anomaly detection for AI agents' mitigation)

**Why it works:** DDoS attacks overwhelm APIs by sending massive amounts of traffic from distributed sources, often bypassing simple rate limiting. Layered defenses at the network, edge, and application levels ensure that APIs continue operating despite large-scale attack attempts.

**Examples:**

- A botnet sends millions of requests per second to a framework’s discovery API.
- Cloudflare DDoS Protection scrubs malicious traffic before it reaches the service.
- AWS Shield Advanced and Google Cloud Armor mitigate volumetric floods at scale.
- Kong API Gateway with WAF plugin enforces request filtering at the application layer.
- Auto-scaling ensures legitimate client requests are still served.

**Addresses:** [Denial of Service on Framework APIs](threat-details.md#denial-of-service-on-framework-apis)

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

**Addresses:** [Lateral Movement - Cross-Layer](threat-details.md#lateral-movement---cross-layer); [Server Side Request Forgery (SSRF)](threat-details.md#server-side-request-forgery-ssrf)

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

## Detect and mitigate bias in security AI agents

*Detective*

Ensure security AI agents operate fairly and do not systematically underprotect or over-monitor certain systems, users, or environments due to biased data or logic.

**How to implement:**

- Audit training data for underrepresented asset types, regions, or patterns.
- Test detection outputs for disparities across entity classes.
- Apply fairness constraints or rebalancing during model training.
- Add explainability tools (e.g., SHAP, LIME) to review agent decisions.
- Log and review false negatives/positives by category to reveal gaps.

**Why it works:** Security agents trained on biased data may overlook critical systems or unfairly over-monitor others. Validating model behavior for fairness and visibility ensures consistent protection, reduces blind spots, and avoids discrimination-based compliance violations.

**Examples:**

- an intrusion detection model underdetects lateral movement in Linux environments.
- Engineers rebalance the training set and Use SHAP to confirm equal threat weightings across OS types.
- monitoring tools flag imbalanced detection rates over time.

**Addresses:** [Bias in Security AI Agents](threat-details.md#bias-in-security-ai-agents)

## Detect and prevent backdoors in AI frameworks

*Preventive*

Establish controls to detect, prevent, and respond to hidden or malicious functionalities intentionally inserted into AI frameworks or their dependencies. Combine code integrity checks, multi-layer review, and runtime attestation to ensure no unauthorized backdoors are present.

**How to implement:**

- Perform independent code audits for framework updates and critical modules.
- Enforce multi-party review (e.g., "four eyes principle") for commits, artifacts, or dependency changes.
- Implement runtime integrity attestation to verify that deployed binaries match audited code (Refer to 'Secure security agent control plane and runtime attestation' mitigation).
- Use static and dynamic analysis tools to flag suspicious or anomalous logic beyond known vulnerability patterns.
- Apply behavioral monitoring to detect unexpected agent actions indicative of hidden backdoors ( Refer to 'Implement behavioral monitoring and anomaly detection for AI agents' mitigation)
- Maintain cryptographic signing and verification of framework builds.

**Why it works:** Backdoors differ from traditional vulnerabilities because they are intentionally hidden by insiders or malicious maintainers. Normal injection-prevention reviews may miss them. By requiring multi-party verification, runtime attestation, and anomaly monitoring, defenders can reduce the chance of undetected backdoor insertion.

**Examples:**

- A malicious framework maintainer inserts hidden functionality that exfiltrates model weights.
- Secondary artifact review (e.g., GitHub branch protection rules, GitLab merge request approvals, Azure DevOps gated check-ins) ensures multi-party sign-off.
- Runtime attestation validates binaries against trusted baselines (Intel SGX/TDX, AMD SEV-SNP, Google Binary Authorization, in-toto).
- Static/dynamic analysis detects anomalous code paths (Semgrep, SonarQube, CodeQL, Veracode SAST/DAST).
- Behavioral monitoring flags unexpected outbound traffic (Falco, Sysdig Secure, Zeek IDS, eBPF-based monitors).
- Cryptographic signing prevents tampered packages from being deployed (Sigstore Cosign, Docker Content Trust, JFrog Artifactory signing, PyPI Trusted Publisher).

**Addresses:** [Backdoor Attacks - AI framework](threat-details.md#backdoor-attacks---ai-framework)

## Detect and prevent lateral movement in AI infrastructure

*Preventive*

Implement dedicated controls to detect, prevent, and misdirect unauthorized movement across AI infrastructure segments. This includes monitoring cross-segment traffic, enforcing fine-grained microsegmentation, and deploying deception mechanisms (honeypots or decoy AI agents).

**How to implement:**

- Monitor east–west traffic within clusters, Service meshes, and between AI agents for anomalies or unexpected communication attempts.
- Enforce microsegmentation at container, pod, and Service levels, ensuring AI workloads can Only communicate with explicitly approved peers.
- Apply zero trust principles: no implicit trust between training, inference, data, and orchestration environments.
- Deploy deception assets such as honeypot model registries, fake datasets, or decoy AI agents in sensitive zones to lure attackers and Provide early detection.

**Why it works:** Lateral movement is a common technique where attackers, once inside, pivot from one compromised service or agent to another. Traditional perimeter defenses rarely detect this behavior because it happens "inside" trusted environments. In AI ecosystems, this could allow an attacker to compromise training data, orchestration platforms, or sensitive models. By combining segmentation, anomaly detection, and deception, defenders can both reduce the blast radius of a compromise and gain visibility into attempted movements.

**Examples:**

- Use Kubernetes network policies, Service mesh rules (Istio, Linkerd), or cloud VPC controls to Restrict flows.
- detect anomalies with IDs/NDR (Zeek, Suricata, Darktrace) and SIEM/SOAR.
- Deploy honeypots or decoy model registries (Canarytokens, OpenCanary, Attivo) for early detection.

**Addresses:** [Lateral Movement - AI infrastructure](threat-details.md#lateral-movement---ai-infrastructure); [Lateral Movement - Cross-Layer](threat-details.md#lateral-movement---cross-layer)

## Detect and respond to AI data exfiltration attempts

*Detective*

Deploy specialized mechanisms to identify, disrupt, and contain attempts to exfiltrate sensitive AI data (datasets, embeddings, model weights, provenance logs) that bypass existing access controls, sandboxing, or encryption. This includes advanced monitoring, deception, throttling, and automated response capabilities.

**How to implement:**

- Define and enforce strict outbound traffic policies at both the network and application layers to prevent unauthorized data transfers.
- Continuously profile normal data access and query patterns, and flag anomalies such as unusual query volumes, off-hours access, or bulk extractions (refer to Implement behavioral monitoring and anomaly detection for AI agents mitigation).
- Implement rate limiting on data flows: apply API-level limits and throttling at storage/query layers (e.g., vector databases, model registries) to disrupt large-scale data pulls.
- Utilize deception mechanisms such as honeytokens, decoy datasets, or watermarked models to detect and trace exfiltration attempts.
- Integrate exfiltration alerts with SIEM/SOAR platforms to trigger automated containment actions (e.g., session termination, key revocation, network isolation).
- Enable detailed packet capture, query logging, and egress metadata collection to support forensic investigation of attempted data theft.
- Route all outbound data through monitored choke points to centralize detection, enforcement, and response.

**Why it works:** While access control, sandboxing, and encryption reduce exfiltration risk, sophisticated adversaries often exploit legitimate channels or mimic authorized use. Dedicated exfiltration defenses ensure organizations can detect theft in progress, slow it down, and respond before large volumes of data are lost. Deception techniques provide early warning, while egress monitoring and automated workflows deliver rapid containment and forensic insight.

**Examples:**

- Zeek IDs or Suricata deployed at egress points to flag abnormal outbound flows.
- cloud-native controls like AWS GuardDuty, Azure Defender for cloud, and GCP VPC Service controls to Enforce data egress restrictions.
- Honeytokens/Canarytokens embedded in sensitive datasets, triggering alerts if accessed externally.
- Elastic SIEM correlates abnormal vector DB query bursts with outbound traffic anomalies.
- SOAR solutions (Splunk Phantom, Palo Alto Cortex XSOAR) Automatically revoke credentials and isolate affected workloads.
- digital watermarking on models detects unauthorized redistribution after exfiltration.

**Addresses:** [Data Exfiltration](threat-details.md#data-exfiltration)

## Detect backdoors during model acquisition, training, and validation

*Detective*

Detect hidden trigger behaviors in AI models during acquisition, training, and validation stages. Backdoors may activate under specific inputs, such as a special token ("cf97x") causing misclassification, a hidden phrase in a prompt triggering harmful outputs, or a watermarked image bypassing moderation filters. Early detection ensures compromised models or poisoned datasets are not promoted into production.

**How to implement:**

- provenance & attestation (Acquisition): Require signed artifacts, hash checks, and SBOM lineage before adoption.
- dataset forensics (training): Apply activation clustering, spectral signatures, and outlier analysis to detect poisoned samples.
- trigger Discovery (validation): Run adversarial Prompt sweeps, Neural Cleanse–style inversion, and token sequence testing to Identify potential backdoor triggers.
- model forensics: Compare saliency maps, neuron activations, and checkpoint weight deltas to detect unusual changes.
- Regression testing: Maintain a library of known backdoor probes and Run them against models before deployment.

**Why it works:** Backdoors are often introduced during data poisoning or supply chain compromise, activating only when specific triggers are present. Detecting them early in the lifecycle prevents malicious models from reaching production. By combining provenance checks, dataset forensics, adversarial probing, and regression tests, organizations can proactively identify hidden triggers before they impact users or downstream agents.

**Examples:**

- Provenance & signing: Sigstore Cosign, in-toto attestations, MLflow Model Registry with hash checks.
- Dataset forensics: IBM Adversarial Robustness Toolbox (Spectral Signatures, Activation Clustering).
- Trigger discovery: TrojanZoo, Neural Cleanse, garak for LLM prompt sweeps.
- Validation: Great Expectations or TensorFlow Data Validation for anomaly detection in datasets.

**Addresses:** [Backdoor Attacks - AI model](threat-details.md#backdoor-attacks---ai-model)

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

**Addresses:** [Horizontal/Vertical Solution Vulnerabilities](threat-details.md#horizontalvertical-solution-vulnerabilities)

## Differential Privacy and Embedding Sanitization

*Preventive*

Apply differential privacy or embedding-space noise injection during vector generation to limit the amount of recoverable semantic information in each embedding, reducing the risk of attackers reconstructing original text from exposed vectors.

**Addresses:** [Embedding Inversion / Reconstruction](threat-details.md#embedding-inversion--reconstruction)

## Disable HTTP redirections and implement a robust URL parser for client input validation.

*Preventive*

Disable HTTP redirections and implement a strong URL parser to validate and sanitize all client input.

**How to implement:**

- Disable support for automatic or client-triggered HTTP redirections to prevent unvalidated forwarding.
- Use a strict URL parser that fully normalizes and validates input before any processing.
- Validate input URLs against expected schemes and domains early in the request pipeline.
- Detect and reject malformed or obfuscated URL input (e.g., encoded redirects).
- Log attempted redirections and URL parsing errors for monitoring and investigation.

**Why it works:** The implementation disables automatic HTTP redirection handling in the application layer to prevent open redirect and SSRF risks. A robust URL parser is integrated early in the input validation process to fully normalize and validate all incoming URL data. The parser ensures that only expected schemes and domains are processed and blocks malformed or obfuscated input, such as encoded redirects. Logs are generated for redirection attempts and invalid URLs to support audit and threat detection.

**Examples:**

- NGINX with Custom rules: Blocks redirection responses and Validates URL patterns.
- OWASP Java Encoder or similar libraries: Enforce strict URL normalization and parsing.
- Express.js with Custom Middleware: Inspects incoming URLs to Reject redirects and malformed input.
- Azure API Management: allows configuring validation rules to block unsafe redirection behaviors.

**Addresses:** [Server Side Request Forgery (SSRF)](threat-details.md#server-side-request-forgery-ssrf)

## Document API endpoints

*Detective*

Maintain comprehensive and up-to-date documentation of all API endpoints, including their methods, parameters, expected responses, authentication requirements, and versioning. Clear documentation helps developers integrate securely, supports consistency, and reduces the risk of misconfiguration or misuse.

**How to implement:**

- Use Standard formats like OpenAPI or Swagger for structured API documentation.
- ensure documentation includes authentication, rate limits, and error codes.
- version documentation alongside API updates to Maintain clarity.
- Make documentation accessible to authorized developers via internal portals.
- Establish a Review process to Keep API documentation accurate and current.

**Why it works:** Effective documentation defines the structure and behavior of API endpoints, enabling consistent implementation and secure integration. Using formal specifications, such as OpenAPI, helps ensure clarity across teams and systems. Versioned documentation reduces integration risks during updates and supports lifecycle management.

**Examples:**

- Swagger/OpenAPI: Define and generate Interactive API docs.
- Postman: publish and share API specs with development teams.
- Redoc: Render OpenAPI files into developer-friendly docs.
- Stoplight: Provides Design, documentation, and mock API tools.
- Insomnia: Offers API Design, debugging, and collaborative documentation.

**Addresses:** [Improper Inventory Management](threat-details.md#improper-inventory-management)

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

**Addresses:** [Spoofing](threat-details.md#spoofing); [Unsafe Consumption of APIs](threat-details.md#unsafe-consumption-of-apis)

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

**Addresses:** [Data Leakage](threat-details.md#data-leakage); [Information Disclosure](threat-details.md#information-disclosure); [Tampering](threat-details.md#tampering)

## Enforce code integrity and supply chain security for AI agents

*Preventive*

Ensure that all AI agent code is authentic, verified, and free from malicious or vulnerable components before deployment.

**How to implement:**

- Require digital code signing for agents. Unsigned or altered code can’t be trusted. Use cryptographic signatures from trusted certificate authorities and Enforce verification during Build and deployment.
- scan dependencies for vulnerabilities or tampering. third-party libraries may hide risks. automate scanning with tools like OWASP Dependency-Check or Snyk in CI/CD pipelines and block builds if high-risk issues are found.
- Deploy Only from immutable, trusted packages. Mutable deployments can be Compromised post-release. Package agents in read-Only containers or signed images, ensuring Only approved builds can Run in production.

**Why it works:** Maintaining code integrity prevents compromised or malicious agents from entering the ecosystem. This is achieved by verifying digital signatures, scanning supply chain dependencies for threats, and using tamper-evident deployment packages to ensure agents remain trustworthy after release.

**Examples:**

- Sign agents with a trusted CA certificate, scan dependencies using Snyk or OWASP Dependency-Check, and deploy via read-only containers.

**Addresses:** [Compromised Agents](threat-details.md#compromised-agents); [Supply Chain Attacks](threat-details.md#supply-chain-attacks); [Supply Chain Attacks - Cross-Layer](threat-details.md#supply-chain-attacks---cross-layer)

## Enforce Control/Data Plane Separation

*Preventive*

Create strict architectural and policy boundaries between the Control and Data Planes. Ensure that communication between them is limited, monitored, and governed by access policies to reduce lateral movement and minimize blast radius from data plane compromises.

**How to implement:**

- Design Separate trust zones for control and data plane components
- Restrict cross-plane communication using network Policy/firewalls
- Log all traffic between control and data planes
- Monitor for unauthorized lateral movement - ensure services in the data plane cannot escalate into control plane

**Why it works:** Create separate network domains for control and data components. Limit communication across planes using firewall rules and ACLs. Ensure the control plane has visibility into the data plane but not vice versa. Monitor cross-plane interactions and apply zero-trust principles to all inter-component communicatio

**Examples:**

- Cisco SD-access for defining control/data zones
- Kubernetes network policies for restricting pod-plane communication
- AWS Security Groups and NACLs for separating control and data resources
- Istio or Service mesh to Restrict east-west traffic across services

**Addresses:** [Data Leakage](threat-details.md#data-leakage)

## Enforce least privilege access for LLMs

*Preventive*

Enforce strict access controls for LLMs by granting only essential API tokens and permissions needed for specific functions. Limit access to backend systems to the minimum required for operation, ensuring that LLMs cannot execute unauthorized actions or access sensitive information.

**How to implement:**

- Identify and document all LLM interactions with systems and data.
- Define clear access Scopes for each Use case and assign the minimum required permissions.
- regularly Audit API tokens and access logs to detect over-privileged configurations.
- Use role-based access control and token expiration policies.
- Continuously Review and update permissions as system requirements evolve.

**Why it works:** Implement role-based access control (RBAC) to assign LLMs only the permissions required for their functions. Define scoped API tokens to limit access to necessary resources. Continuously monitor access logs and usage patterns with automated alerts for anomalies. Periodically review and update permissions to reflect changes in system behavior and evolving threat landscapes

**Examples:**

- API Management tools such as AWS API gateway, Azure API Management to Enforce access control and rate limits.
- Deploy WAFs such as Cloudflare, AWS WAF to inspect HTTP traffic for threats.
- RBAC solutions like Okta, Auth0 to manage permissions and Enforce least privilege.
- Content filtering tools such as Sift, Microsoft Content Moderator to analyze and block harmful user inputs.

**Addresses:** [Denial of Service (DoS) Attacks - AI model](threat-details.md#denial-of-service-dos-attacks---ai-model); [Direct prompt injection](threat-details.md#direct-prompt-injection); [Indirect prompt injection](threat-details.md#indirect-prompt-injection); [Membership Inference Attacks](threat-details.md#membership-inference-attacks); [Model Stealing](threat-details.md#model-stealing); [Rogue LLM Instructions](threat-details.md#rogue-llm-instructions); [User-driven prompt injection](threat-details.md#user-driven-prompt-injection)

## Enforce Metadata-Stripping and Schema-Controlled Retrieval Outputs

*Preventive*

Configure retrievers to return only approved fields and automatically strip file paths, owners, timestamps, and non-content metadata before results are passed to downstream components. This prevents structural or sensitive metadata from ever leaving the retrieval layer.

**Addresses:** [Metadata leakage](threat-details.md#metadata-leakage)

## Enforce SBOM for AI supply chain security

*Preventive*

Maintain and verify a Software Bill of Materials (SBOM) for all AI components, including libraries, models, containers, and pipelines, to detect vulnerable, malicious, or unauthorized dependencies and reduce the risk of cross-layer supply chain compromise.

**How to implement:**

- Generate SBOMs for all AI software artifacts (libraries, models, containers, infrastructure code).
- Validate SBOMs against vulnerability databases (e.g., NVD, OSV).
- Require SBOM submission from third-party vendors and model providers.
- Integrate SBOM checks into CI/CD pipelines for automated validation.
- Continuously monitor SBOM entries for newly disclosed vulnerabilities or supply chain compromises.
- Correlate SBOM entries with integrity checks (signatures, hashes) to ensure components are not tampered.
- Store SBOMs in a secure, versioned repository for auditability and compliance.

**Why it works:** Supply chain attacks exploit hidden or vulnerable dependencies. By enforcing SBOM practices, organizations gain full visibility into the components that make up their AI systems, enabling them to detect when a compromised library, container, or model is in use. SBOMs also provide a foundation for continuous monitoring and compliance reporting under frameworks like NIST AI RMF and EU AI Act.

**Examples:**

- Syft/Grype generate and scan SBOMs for vulnerabilities.
- CycloneDX or SPDX formats Provide Standard SBOM representation.
- Anchore or JFrog Xray Integrate SBOM validation into CI/CD pipelines.
- in-toto attestation ties SBOMs to Build provenance.
- HuggingFace model cards with hash validation ensure pre-trained model integrity.

**Addresses:** [Backdoor Attacks - AI model](threat-details.md#backdoor-attacks---ai-model); [Supply Chain Attacks - Cross-Layer](threat-details.md#supply-chain-attacks---cross-layer)

## Enforce Strict Authenticated Cache Writes with Provenance Validation

*Preventive*

Only trusted, authenticated services should be able to write to or update cache entries, and each entry must include verified provenance metadata (source ID, signatures, pipeline version). This prevents attackers or untrusted components from injecting or modifying cached vectors or semantic content.

**Addresses:** [Cache Poisoning (semantic or vector cache)](threat-details.md#cache-poisoning-semantic-or-vector-cache)

## Enforce usage policy and detect unauthorized fine-tuning

*Preventive*

Prevent reprogramming attacks by enforcing strict usage policies for AI models and detecting unauthorized fine-tuning that attempts to repurpose models for malicious tasks. This ensures that models are only used within their declared scope and that any attempts to re-task them are detected and blocked before deployment or during runtime.

**How to implement:**

- Use policy enforcement and define acceptable use cases for each model, document them, and enforce policies at orchestration and API layers.
- Require models to be registered with metadata (intended purpose, allowed tasks, approved datasets) before deployment.
- Monitor fine-tuning activity, compare new model checkpoints against the base model, and flag large behavioral or distributional shifts.
- Require human approval for fine-tuning requests, especially those involving sensitive or high-risk tasks.
- Embed task-specific constraints and guardrails into model wrappers (e.g., allowed APIs, restricted vocabulary).
- Test models against adversarial inputs to assess susceptibility to reprogramming (e.g., coercive prompts, adversarial re-tasking inputs).

**Why it works:** Reprogramming attacks occur when models are intentionally or unintentionally re-tasked to perform malicious operations, bypassing their original purpose. While runtime controls limit misuse, policy enforcement and checkpoint validation ensure models cannot be repurposed in the supply chain or during unauthorized fine-tuning. Detecting behavioral shifts, enforcing registries, and validating against declared tasks help organizations ensure model integrity and prevent harmful re-tasking.

**Examples:**

- usage enforcement: Open Policy Agent (OPA), Kong gateway, Istio RBAC to Enforce model Use policies.
- model Registry: MLflow, Vertex AI model Registry with purpose/metadata tags.
- fine-Tune detection: checkpoint comparison tools like WeightWatcher, DeepInspect, or model fingerprinting.
- approval workflows: GitOps or CI/CD pipelines with human Review steps for new model versions.
- red team testing: MITRE Atlas adversarial scenarios, garak for LLM coercion testing.

**Addresses:** [Reprogramming Attacks](threat-details.md#reprogramming-attacks)

## Ensure accountability for AI agents

*Detective*

Ensure that all actions performed by AI agents are traceable, provable, and tamper-resistant, so agents cannot deny responsibility for their behavior. For example, every action must be logged immutably and linked to the agent’s verified identity.

**How to implement:**

- implement immutable logging: Store records in append-Only systems or Blockchain-backed ledgers to prevent tampering.
- Use cryptographic signatures: Require agents to sign actions or transactions with their private keys for attribution.
- Maintain provenance chains: track the full chain of requests, responses, and tool usage so every decision can be linked back to the originating agent.

**Why it works:** Repudiation creates accountability gaps that attackers can exploit. By combining tamper-resistant logs, cryptographic non-repudiation, and clear provenance records, systems can ensure that every action is attributable to the correct agent and cannot be denied later.

**Examples:**

- An AI agent’s actions are logged in an append-only ledger (AWS QLDB or Hyperledger Fabric) with digital signatures applied using its private key. Provenance metadata is captured in Elasticsearch, enabling full traceability of all API calls and responses.

**Addresses:** [Repudiation - AI agent](threat-details.md#repudiation---ai-agent)

## Ensure availability and resilience of AI agent evaluation infrastructure

*Preventive*

Ensure that evaluation systems, such as model validation pipelines, test harnesses, and benchmark execution environments, used to test and validate AI agents, remain available and tamper-resistant, even under targeted denial-of-service or degradation attacks.

**How to implement:**

- Deploy evaluation services in high-availability (HA) clusters to avoid single points of failure during load spikes or system crashes.- Use load balancing, rate limiting, and network segmentation to isolate abuse.
- Apply rate limiting and request throttling to prevent abuse or automated flooding of model validation endpoints.
- Use network segmentation or service mesh isolation to separate evaluation environments from external-facing infrastructure.
- Monitor evaluation system uptime, latency, and error rates, and alert on performance degradation or failed jobs.
- Version and back up all test data, benchmarks, and evaluation artifacts in redundant storage systems (e.g., S3 with versioning, IPFS, Git-backed storage).
- Implement circuit breakers and fallback mechanisms that allow minimal evaluation flows (e.g., canary tests) to run even if full pipelines fail

**Why it works:** If attackers disrupt AI evaluation tools, compromised agents may bypass testing or remain unverified. Making evaluation systems resilient ensures performance and safety checks are not skipped or silently disabled, preserving trust in security outcomes.

**Examples:**

- A SOC’s CI/CD pipeline evaluates every security agent update using distributed runners and cached benchmarks. Rate limits protect the model API from overload. A circuit breaker ensures fallback tests run if the main evaluator times out. Logs and artifacts are stored in versioned, replicated storage.

**Addresses:** [Denial of Service on Evaluation Infrastructure](threat-details.md#denial-of-service-on-evaluation-infrastructure)

## Ensure resilience of AI data infrastructure against DOS attacks

*Preventive*

Harden and monitor AI data infrastructure to withstand denial-of-service conditions by combining redundancy, load balancing, caching, and query-level protections to ensure continued availability for critical AI agent operations.

**How to implement:**

- Implement redundancy and failover for data stores (multi-region replication, read replicas).
- Deploy caching layers (Redis, Memcached) to reduce dependency on primary stores during spikes.
- Apply query-level safeguards: rate limiting, query complexity thresholds, and resource quotas.
- Prioritize mission-critical AI agent queries over bulk or non-essential workloads.
- Monitor for DoS patterns at the storage/query layer, not just at APIs.
- Use auto-scaling and elastic infrastructure to absorb sudden increases in load.
- Conduct resilience testing and chaos engineering to validate data availability under attack conditions

**Why it works:** DoS on data infrastructure specifically targets the backbone of AI functionality, which is the data. While API-level protections defend service endpoints, databases, and pipelines also need resilience. By combining caching, replication, query safeguards, and chaos testing, organizations can ensure that AI agents maintain functionality even under attack.

**Examples:**

- Use AWS Aurora multi-AZ or Google cloud Spanner for database replication and failover.
- Deploy Redis caching to reduce load on vector DBs during traffic spikes.
- Configure PostgreSQL query limits or Elasticsearch circuit breakers to prevent resource exhaustion.
- Apply Istio Service mesh policies to Prioritize critical Agent queries.
- Use Gremlin or Chaos mesh for resilience/Chaos testing of data pipelines.

**Addresses:** [Denial of Service on Data Infrastructure](threat-details.md#denial-of-service-on-data-infrastructure)

## Establish agent identity and trust verification

*Preventive*

Implement mechanisms to confirm that all AI agents are legitimate through cryptographic identity checks and trust validation.

**How to implement:**

- Require mutual authentication between agents and orchestrators using cryptographic certificates or signed tokens.
- implement a secure registration process where each agent’s origin, owner, and code signature are verified before onboarding.
- Revalidate Agent credentials Periodically, not just at onboarding, to detect hijacking or credential theft.

**Why it works:** Verifying identity ensures only trusted agents can operate, reducing infiltration risks. This is achieved by using digital certificates, signed tokens, and regular credential rotation, which provide strong assurance that agents remain authentic over time.

**Examples:**

- Use X.509 certificates for agent–orchestrator authentication, combined with certificate rotation every 30 days.

**Addresses:** [Agent Identity Attack](threat-details.md#agent-identity-attack); [Agent Impersonation](threat-details.md#agent-impersonation); [Compromised Agents](threat-details.md#compromised-agents); [Framework Evasion](threat-details.md#framework-evasion)

## Establish alignment verification gates for agent outputs

*Preventive*

Implement verification gates that evaluate agent outputs against defined schemas, policies, and alignment requirements before those outputs are consumed by downstream agents or used to trigger actions. These gates act as checkpoints to prevent misaligned goals from propagating across multi-agent ecosystems.

**How to implement:**

- Schema enforcement: Validate outputs against strict response schemas (e.g., JSON Schema, Pydantic) to prevent accidental exposure of unintended fields.
- Policy checks: Use policy engines (e.g., OPA, Casbin, Cedar) to verify that the output aligns with agent permissions, allowed actions, and data classification rules.
- Safety & privacy filtering: Scan outputs for sensitive data (PII, secrets), unsafe instructions, or adversarial payloads. Apply redaction or sanitization when required.
- Factuality & grounding: Verify claims against trusted sources or require citations; flag low-confidence outputs for human review.
- Risk-based routing: Define outcomes (allow, transform, block, or send to human-in-the-loop) based on risk classification.
- Tamper resistance: Sign validated outputs with cryptographic signatures to ensure downstream agents only process verified content.
- Audit logging: Maintain immutable logs of inputs, checks applied, and final decisions for traceability and compliance.

**Why it works:** Misaligned agent outputs can propagate harmful or erroneous goals to other agents. Alignment verification gates act as policy-driven guardrails, ensuring outputs are structurally valid, policy-compliant, safe, and aligned with system goals before they are passed downstream. This prevents cascading misalignment across agent ecosystems.

**Examples:**

- Schema validation: JSON Schema or Pydantic for strict output enforcement.
- Policy enforcement: Open Policy Agent (OPA) to Validate actions against defined rules.
- Safety scanning: Microsoft Presidio or secret scanning tools to redact sensitive data.
- Factuality verification: Retrieval-and-verify workflows or grounding against trusted KBs.
- routing: Kong gateway or Istio EnvoyFilter plugins to intercept and gate outputs before transmission.
- approval queue: Integration with Airflow, Kubeflow, or human Review dashboards for high-risk outputs.

**Addresses:** [Backdoor Attacks - AI model](threat-details.md#backdoor-attacks---ai-model); [Goal Misalignment Cascades](threat-details.md#goal-misalignment-cascades); [Reprogramming Attacks](threat-details.md#reprogramming-attacks)

## Establish governance and auditability for AI agents

*Detective*

Create oversight mechanisms to track, review, and revoke AI agent activity to maintain accountability and trust.

**How to implement:**

- Implement immutable audit logging: Compromised agents may erase traces. Store logs in append-only systems with cryptographic verification to ensure integrity.
- Sanitize logs to prevent exposure of secrets or personal data. Use structured logging with redaction policies and RBAC for dashboard access.
- Create a security certification process: Without validation, insecure agents may be deployed. Align reviews with ISO 27001, ISO 27034, NIST SP 800-53, OWASP ASVS, and AI-specific frameworks such as the EU AI Act, NIST AI Risk Management Framework, and OECD AI Principles.
- Maintain a kill switch for malicious agents: Delayed response increases damage. Provide administrators with the ability to instantly disable or remove untrusted agents.

**Why it works:** Governance ensures agents remain transparent and accountable. This is achieved by securing logs, certifying agent compliance, and maintaining rapid-response capabilities to revoke or disable agents when necessary. Governance also includes protecting observability data to avoid leakage of sensitive agent inputs, outputs, or credentials.

**Examples:**

- Use immutable log storage with AWS CloudTrail or Elasticsearch, perform quarterly reviews against ISO 27001 and NIST AI RMF requirements, and include EU AI Act conformity assessments for high-risk systems. Provide a central control panel with a kill switch to revoke malicious AI agents.

**Addresses:** [Agent Identity Attack](threat-details.md#agent-identity-attack); [Agent Impersonation](threat-details.md#agent-impersonation); [Agent Tool Misuse](threat-details.md#agent-tool-misuse); [Compromised Agents](threat-details.md#compromised-agents); [Data Exfiltration](threat-details.md#data-exfiltration); [Data Leakage through Observability](threat-details.md#data-leakage-through-observability); [Framework Evasion](threat-details.md#framework-evasion)

## Evaluate service provider API security

*Detective*

Assess the security of your service provider’s API by evaluating their authentication, encryption, and access control mechanisms. Ensure their practices align with industry standards and your application’s risk requirements. Confirm that the API supports secure transmission and handles errors gracefully.

**How to implement:**

- Review API documentation for authentication, encryption, error handling, and rate limits.
- Evaluate the provider’s API under different conditions to test reliability and performance.
- Confirm compatibility with your system and review support and update policies.
- Check for logging capabilities and incident response procedures.
- Ensure the provider uses secure protocols (e.g., OAuth 2.0, TLS).

**Why it works:** Evaluating service provider API security involves reviewing documentation and conducting functional tests under real-world conditions. The goal is to ensure secure access, proper error handling, scalability, and resilience to attacks. This helps confirm that the API can be a sustainable and secure part of your architecture.

**Examples:**

- Postman: for testing API functionality, rate limiting, and authentication.
- OWASP ZAP: Open-source tool for scanning APIs for vulnerabilities.
- AWS API gateway: Offers built-in support for authentication, throttling, and logging.
- Azure API Management: Enables secure access, monitoring, and access control.
- Google cloud Apigee: Provides API analytics, Policy enforcement, and threat protection.

**Addresses:** [Unsafe Consumption of APIs](threat-details.md#unsafe-consumption-of-apis)

## Fine-tune the LLM for accuracy

*Preventive*

Use domain-specific data and techniques like prompt engineering, parameter-efficient tuning, and chain-of-thought prompting to improve LLM accuracy. Regularly evaluate and update the model to maintain high-quality, trustworthy responses.

**How to implement:**

- Validate high-stakes outputs through human oversight.
- create user feedback loops to flag inaccurate results.
- Use confidence scoring systems to signal response reliability.
- Integrate trusted APIs and data sources for Fact-checking.
- Audit and retrain models regularly using updated datasets.
- Educate users on LLM limitations and expected output quality.

**Why it works:** Fine-tuning involves training the LLM on high-quality, domain-specific datasets to improve relevance and accuracy. Techniques like prompt engineering guide the model toward more precise outputs. Confidence scoring systems offer reliability insights to users. Continuous updates based on new data, auditing outcomes, and user feedback ensure the model improves over time.

**Examples:**

- OpenAI: Offers fine-tuning capabilities for GPT models using domain-specific data.
- Google's BERT: Supports fine-tuning for specific NLP tasks.
- Hugging Face Transformers: Provides libraries for domain-specific model training.
- Snorkel: Enables programmatic data labeling to improve fine-tuning datasets.
- Weights & Biases (W&B): Tracks model performance during and after fine-tuning.

**Addresses:** [Data Poisoning - Training Phase](threat-details.md#data-poisoning---training-phase); [Inaccurate LLM information](threat-details.md#inaccurate-llm-information)

## Harden and monitor orchestration platforms for AI agents

*Preventive*

Secure the orchestration layer (e.g., Kubernetes, Docker, ECS) responsible for deploying and managing AI agents. Implement runtime hardening, network isolation, access controls, and live monitoring to prevent abuse of orchestration features and lateral movement.

**How to implement:**

- Harden Kubernetes API server with authentication, RBAC, and audit logging.
- Enforce Pod Security Standards (PSS) and prevent privileged containers.
- Use runtime monitoring tools (e.g., Falco, Sysdig Secure) to detect container escape, namespace injection, or tampering.
- Isolate AI agent workloads using namespaces, network policies, and taints/tolerations.
- Limit access to orchestration metadata endpoints (e.g., Kubelet, cloud instance metadata).
- Validate orchestration configurations pre-deploy using tools like OPA/Gatekeeper.

**Why it works:** While configuration assessments catch static misconfigurations, orchestration systems remain vulnerable to runtime exploits and control-plane abuse. Hardening Kubernetes, limiting permissions, isolating workloads, and monitoring runtime behavior are essential to defend against attackers exploiting orchestration APIs to compromise or control AI agents.

**Examples:**

- Use OPA Gatekeeper to block privileged containers, apply Calico network policies to restrict pod communication, and deploy Falco to detect suspicious syscalls or container escapes in real-time.

**Addresses:** [Lateral Movement - Cross-Layer](threat-details.md#lateral-movement---cross-layer); [Orchestration Attacks](threat-details.md#orchestration-attacks)

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

**Addresses:** [Security Misconfiguration (API)](threat-details.md#security-misconfiguration-api)

## Harden identity and authorization mechanisms for AI agents

*Preventive*

Protect the identity, credentials, and authorization of AI agents from compromise, ensuring that attackers cannot gain unauthorized control.

**How to implement:**

- Secure credential handling Avoid embedding secrets in code or config files. Store them in a secrets manager or HSM and automate rotation through CI/CD pipelines.
- Protect tokens and sessions Use short-lived, renewable tokens tied to agent identity and environment. Enforce automatic expiration and revoke tokens if suspicious activity is detected.
- Strengthen authorization checks Replace static role checks with fine-grained, policy-based access control (ABAC or policy-as-code). Continuously evaluate agent context such as origin, purpose, and behavior before allowing access.

**Why it works:** Identity attacks succeed when agents rely on weak or static authentication. Hardening defenses ensures that even if attackers steal or replay credentials, their use is limited or blocked. This is achieved with secure storage, continuous session validation, and adaptive authorization policies.

**Examples:**

- An AI agent stores credentials in HashiCorp Vault, rotates them every 24 hours, and uses short-lived OAuth2 tokens bound to the agent’s certificate and runtime environment. Authorization is enforced via policy-as-code with Open Policy Agent (OPA).

**Addresses:** [Agent Identity Attack](threat-details.md#agent-identity-attack); [Model Stealing](threat-details.md#model-stealing)

## Implement a Security Information and Event Management (SIEM) solution.

*Detective*

Deploy a Security Information and Event Management (SIEM) solution to collect and analyze log data from systems, applications, and network devices. SIEMs help categorize incidents, detect threats, and improve response capabilities across the organization.

**How to implement:**

- Collect logs from all Key systems and devices
- Tune Log levels to capture critical events efficiently - update logging policies as new threats emerge
- Enable Real-time alerts for suspicious activity
- Audit logs regularly to verify retention and integrity
- Train teams on SIEM tools and incident response processes

**Why it works:** A SIEM collects and analyzes logs from systems, applications, and networks to detect threats and support incident response. It uses rules and anomaly detection to flag suspicious activity in real time. Logs are stored securely, and regular audits ensure data integrity, policy compliance, and effective threat visibility across the environment.

**Examples:**

- Splunk / LogRhythm / IBM QRadar: Enterprise SIEM platforms with alerting and dashboards
- ELK Stack / Graylog: Open-source tools for Log ingestion, analysis, and visualization
- Microsoft Sentinel: cloud-native SIEM with built-in threat detection
- AlienVault OSSIM: Combines SIEM with basic threat intelligence for small teams

**Addresses:** [Compromised Observability Tools](threat-details.md#compromised-observability-tools)

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

**Addresses:** [Bypass Access Control](threat-details.md#bypass-access-control); [Elevation of Privilege](threat-details.md#elevation-of-privilege)

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

**Addresses:** [Broken Function Level Authorization](threat-details.md#broken-function-level-authorization); [Broken Object Level Authorization](threat-details.md#broken-object-level-authorization); [Data Leakage](threat-details.md#data-leakage); [Privilege Escalation](threat-details.md#privilege-escalation)

## Implement API rate limiting

*Preventive*

Enforce API rate limits to cap the number of requests per user or IP address within a defined time period. Implement quotas to prevent excessive resource consumption and mitigate Denial of Service risks.

**How to implement:**

- Define clear rate limits based on usage patterns and system capacity.
- implement dynamic rate limiting to adapt to traffic spikes or unusual patterns.
- Use exponential backoff strategies for retrying requests after hitting limits.
- Monitor and Log usage patterns to Identify potential abuse or anomalies.
- Provide users with feedback on rate limits and remaining quota.
- Consider implementing a whitelist for trusted users or applications to allow higher limits.

**Why it works:** API rate limiting uses middleware to inspect request frequency per user or IP. If a request exceeds the set limit, it is rejected with an error. Common methods like token bucket or sliding window algorithms manage request bursts. These limits are enforced dynamically based on load. Logs are analyzed periodically to refine limits.

**Examples:**

- Amazon API gateway: Provides built-in support for rate limiting and throttling to manage API requests.
- Google cloud endpoints: Offers quota Management features to limit API usage per user or project.
- NGINX: can be configured to limit requests per IP address using the limit_req module.
- Kong gateway: allows for rate limiting plugins to Enforce request limits on APIs.
- Redis: can be used for implementing Custom rate limiting logic with its in-memory data structure capabilities.

**Addresses:** [Denial of Service (DoS) Attacks - AI infrastructure](threat-details.md#denial-of-service-dos-attacks---ai-infrastructure); [Denial of Service on Framework APIs](threat-details.md#denial-of-service-on-framework-apis); [LLM Denial of Service](threat-details.md#llm-denial-of-service); [Model Stealing](threat-details.md#model-stealing); [Resource Hijacking](threat-details.md#resource-hijacking); [Unrestricted Resource Consumption](threat-details.md#unrestricted-resource-consumption)

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

**Addresses:** [Broken Function Level Authorization](threat-details.md#broken-function-level-authorization); [Broken Object Level Authorization](threat-details.md#broken-object-level-authorization); [Bypass Access Control](threat-details.md#bypass-access-control); [Elevation of Privilege](threat-details.md#elevation-of-privilege)

## Implement behavioral monitoring and anomaly detection for AI agents

*Detective*

Continuously observe AI agent activity to detect and respond to suspicious or malicious behaviors in real time.

**How to implement:**

- Implement real-time behavior monitoring using telemetry, logs, and agent audit trails. Track API calls, resource usage, and output patterns to detect deviations from expected behavior profiles.
- Define and enforce policy-based controls (e.g., RBAC, ABAC) using machine-readable rules. Apply them at runtime to restrict agent capabilities and detect policy violations.
- Validate incoming telemetry at the source, using checksums, attestations, or cross-agent correlation to detect tampered or false observability data.
- Automate threat response actions. When an agent shows suspicious behavior, auto-isolate it, throttle its access, or trigger alerts, and don’t wait for manual review.

**Why it works:** Monitoring agent behavior ensures that even if compromised agents bypass initial checks, they can be detected and contained. This is achieved by combining telemetry, rule-based enforcement, and automated response systems to reduce impact before escalation. If observability inputs are poisoned, detection may fail. Redundancy and input validation help ensure alerts reflect actual agent behavior.

**Examples:**

- Use Prometheus/Grafana for telemetry, OPA for policy enforcement, and Kubernetes Pod Security Policies to isolate suspicious containers.

**Addresses:** [Agent Tool Misuse](threat-details.md#agent-tool-misuse); [Compromised Agents](threat-details.md#compromised-agents); [Data Exfiltration](threat-details.md#data-exfiltration); [Evasion of Detection](threat-details.md#evasion-of-detection); [Framework Evasion](threat-details.md#framework-evasion); [Goal Misalignment Cascades](threat-details.md#goal-misalignment-cascades); [Lateral Movement - AI infrastructure](threat-details.md#lateral-movement---ai-infrastructure); [Model Stealing](threat-details.md#model-stealing); [Poisoning Observability Data](threat-details.md#poisoning-observability-data); [Security Agent Data Poisoning](threat-details.md#security-agent-data-poisoning)

## Implement CAPTCHA for User Verification

*Preventive*

Implement CAPTCHA to verify users and block bots from accessing sensitive business flows. Use challenge-response tests to ensure only legitimate users interact with APIs, reducing the risk of exploitation that could disrupt transactions or manipulate virtual currencies or platform balances.

**How to implement:**

- Use adaptive CAPTCHAs triggered by high-risk activity or anomalies
- Choose CAPTCHA types that balance user friction and Security - update CAPTCHA libraries to address bypass techniques
- Monitor CAPTCHA failure rates and refine thresholds
- Offer accessible verification alternatives (e.g., audio CAPTCHA or OTP)

**Why it works:** CAPTCHA services are triggered by unusual patterns like rapid requests or high-risk actions. The system uses challenge-response prompts (e.g., image or logic tests) to block bots and verify user intent. CAPTCHAs should be adaptive, appearing only when needed, and logs must capture results for anomaly review. Regular updates ensure resistance to evolving bot tactics, while accessibility options help serve all users.

**Examples:**

- Google reCAPTCHA: adaptive CAPTCHA with Bot scoring and visual/audio fallback - hCaptcha: privacy-focused CAPTCHA with customizable challenge types
- Cloudflare Bot Management: detects and mitigates Bot activity in APIs
- Akamai Bot Manager: Enforces CAPTCHA on risky flows with Advanced detection
- Distil networks: integrates CAPTCHA and Bot defenses into sensitive endpoints

**Addresses:** [Unrestricted Access to Sensitive Business Flows](threat-details.md#unrestricted-access-to-sensitive-business-flows)

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

## Implement data sanitization techniques

*Preventive*

Integrate robust data sanitization processes to ensure user data is not included in the training model. Regularly audit and update these processes to maintain effectiveness and prevent data bleed over between users.

**How to implement:**

- Employ differential privacy methods to obscure individual user data.
- implement strict access controls to limit data exposure during training.
- Use data anonymization techniques to Remove personally identifiable information.
- regularly Review and refine data handling policies to adapt to new threats.
- Train staff on data privacy best practices to minimize human error.
- Monitor model outputs for unintended data leakage and adjust training data accordingly.

**Why it works:** Data sanitization techniques preprocess user input to remove sensitive information before it enters the training pipeline. Methods include tokenizing or anonymizing personal identifiers, applying noise for differential privacy, and restricting data access during training. Audits and continuous monitoring help ensure compliance with privacy standards and detect potential data leakage.

**Examples:**

- Google’s Differential Privacy framework, which allows for data analysis while protecting individual user data.
- OpenAI's API employs data usage policies that ensure user inputs are not stored or used for model training.
- Apple’s use of on-device processing and differential privacy to collect data while preserving user anonymity.
- Microsoft’s Azure Confidential Computing, which protects data in use by isolating it in a secure environment.
- Amazon Macie for sensitive data detection.

**Addresses:** [Compromised RAG Pipelines](threat-details.md#compromised-rag-pipelines); [Data Poisoning - AI Agent](threat-details.md#data-poisoning---ai-agent); [Data Poisoning - Training Phase](threat-details.md#data-poisoning---training-phase); [Data Tampering](threat-details.md#data-tampering); [Security Agent Data Poisoning](threat-details.md#security-agent-data-poisoning); [User data bleed over](threat-details.md#user-data-bleed-over)

## Implement Data Version Control

*Corrective*

Use Data Version Control (DVC) to track all dataset changes and enforce strict controls on data integrity. Audit regularly to detect anomalies and prevent unauthorized modifications or data poisoning.

**How to implement:**

- Establish data provenance to trace dataset origins and Identify potential malicious sources.
- implement robust validation for incoming data, including anomaly detection to flag suspicious entries.
- limit individuals with write access, enforcing least privilege.
- conduct regular Security training for data handlers to recognize and report threats.
- Use cryptographic hashing to verify data integrity before and after training.

**Why it works:** DVC implementation creates a system that tracks dataset changes through unique version identifiers. Each version is logged with metadata (timestamps, user actions, etc). Automated anomaly detection algorithms assess incoming data for irregularities. Cryptographic hashing verifies data integrity before and after training, ensuring authenticity. Regular audits review dataset changes and identify potential threats.

**Examples:**

- Examples of technology that implements data version control include:
- DVC (Data Version Control)
- Git LFS (Large File Storage),
- Pachyderm. These tools allow for tracking changes in datasets, maintaining data provenance, and integrating with CI/CD pipelines for automated testing.
- Anomaly detection can be achieved using tools like TensorFlow Data Validation or Apache Spot, while cryptographic hashing can be implemented using libraries such as hashlib in Python.

**Addresses:** [Compromised RAG Pipelines](threat-details.md#compromised-rag-pipelines); [Data Poisoning - AI Agent](threat-details.md#data-poisoning---ai-agent); [Data Tampering](threat-details.md#data-tampering); [Inject malicious stuff into training process](threat-details.md#inject-malicious-stuff-into-training-process); [Malicious pre-training](threat-details.md#malicious-pre-training)

## Implement device fingerprinting to block unauthorized client devices

*Preventive*

Implement device fingerprinting to restrict access to sensitive business flows, ensuring only authorized client devices can interact with APIs.

**How to implement:**

- Use fingerprinting methods that resist spoofing and tampering - adapt fingerprinting algorithms as new devices and threats emerge
- Maintain a trusted device whitelist and Compare fingerprints for access decisions
- Provide secure fallback options for legitimate device changes
- Log device interactions and flag anomalies tied to fingerprint shifts

**Why it works:** Device fingerprinting involves collecting various attributes from client devices, such as browser type, operating system, IP address, screen resolution, and installed plugins. This data is hashed to create a unique identifier for each device. When a device attempts to access sensitive APIs, its fingerprint is compared against a whitelist of authorized devices. Unauthorized devices are blocked, while legitimate users may be prompted for additional verification if their fingerprint changes.

**Examples:**

- FingerprintJS: JS library that generates unique device IDs
- ThreatMetrix: uses deep fingerprinting and behavior data to assess risk
- BioCatch: Combines biometrics and behavior for anomaly detection
- Iovation: Flags fraudulent activity using device profiles
- Arkose Labs: fingerprints and challenges suspicious client environments

**Addresses:** [Unrestricted Access to Sensitive Business Flows](threat-details.md#unrestricted-access-to-sensitive-business-flows)

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

**Addresses:** [Denial of Service](threat-details.md#denial-of-service); [Denial of Service (DoS) Attacks - AI infrastructure](threat-details.md#denial-of-service-dos-attacks---ai-infrastructure); [Lateral Movement - AI infrastructure](threat-details.md#lateral-movement---ai-infrastructure)

## Implement Downstream Authorization Checks

*Preventive*

Implement authorization checks in downstream systems for all high-impact actions. Ensure that every request made through LLM-based applications or plugins is validated against established security policies to prevent excessive autonomy. Enforce the complete mediation principle to guarantee that no action is executed without proper approval.

**How to implement:**

- Define criteria for what constitutes a high-impact action that requires downstream authorization.
- Establish and document Security policies that specify approval thresholds and approvers.
- Design role-based access policies to Define who can authorize which actions.
- ensure the architecture Supports Real-time authorization enforcement.
- Educate stakeholders on the importance of downstream authorization in LLM workflows.

**Why it works:** Downstream authorization checks involve integrating a validation layer within the application architecture that intercepts all requests for high-impact actions. Each request is matched against predefined security policies and user roles. The system employs real-time decision-making algorithms to assess permissions, logging all requests and outcomes for auditing. Role-based access controls ensure that only designated users can approve actions, enhancing accountability and compliance.

**Examples:**

- OAuth 2.0 and OpenID Connect frameworks for managing access tokens and permissions in applications.
- AWS IAM (Identity and Access Management) for defining granular permissions and roles for actions in cloud environments.
- Azure Active Directory for implementing conditional access policies based on user roles and actions.
- ServiceNow for automating approval workflows and tracking authorization requests in enterprise environments.

**Addresses:** [Excessive autonomy](threat-details.md#excessive-autonomy); [Lateral Movement - Cross-Layer](threat-details.md#lateral-movement---cross-layer)

## Implement extreme least privilege access controls

*Preventive*

Implement extreme least privilege access controls by restricting entities and services to the minimum necessary permissions, including specific REST API methods and endpoints. Ensure that privileges are correctly assigned, modified, and tracked to prevent unauthorized actions and limit potential damage from coercion, model theft, and path traversal vulnerabilities.

**How to implement:**

- regularly Audit and Review access permissions
- Enforce RBAC for assigning minimal access per role
- Require MFA for access to sensitive endpoints
- Log and Monitor access to detect unauthorized actions - sanitize and Validate all external inputs
- Restrict rest API calls to authorized methods Only
- Use encryption for sensitive data to prevent exfiltration

**Why it works:** Enforce least privilege by assigning the minimum required permissions to each identity and service. Use centralized authorization to validate REST API calls and restrict access to sensitive endpoints. Maintain access logs and alert on unauthorized activity. Sanitize inputs to block path traversal, and apply MFA for sensitive operations.

**Examples:**

- AWS IAM allows for fine-grained access control to AWS resources, enabling least privilege access through policies.
- Azure active Directory Provides role-based access control (RBAC) for managing user permissions and ensuring minimal access rights.
- Google cloud IAM Enables users to Define roles and permissions, enforcing least privilege access to cloud resources.
- HashiCorp Vault manages secrets and access to sensitive data, ensuring Only authorized entities can retrieve them.

**Addresses:** [Lateral Movement - Cross-Layer](threat-details.md#lateral-movement---cross-layer); [Model theft](threat-details.md#model-theft); [Privilege Escalation](threat-details.md#privilege-escalation)

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

**Addresses:** [Data Poisoning - AI Agent](threat-details.md#data-poisoning---ai-agent); [Data Tampering](threat-details.md#data-tampering); [Tampering](threat-details.md#tampering)

## Implement human approval for high-impact actions

*Preventive*

Require human approval for all high-impact actions in the LLM-based application or plugin. Implement a human-in-the-loop control mechanism to ensure that no significant action is executed without prior verification by a human.

**How to implement:**

- Define clear criteria for what constitutes a high-impact action.
- Establish a streamlined human Review process that balances speed with accountability.
- Train approvers on their role in mitigating risk during the Review process.
- set policies for when approvals are required, including thresholds and exemptions.
- ensure the approval interface is intuitive and accessible for non-technical users.
- Review and update approval policies Periodically based on incident trends and feedback.

**Why it works:** Design a user interface that prompts for human approval before executing high-impact actions, integrating it seamlessly into the existing workflow. Implement a backend system that flags actions based on predefined criteria and routes them to designated approvers. Utilize notifications to alert approvers of pending actions. Ensure logging captures decision details and timestamps. Regularly assess the system's performance and user feedback to refine the approval process.

**Examples:**

- Jira / Trello: Workflow approvals, good for LLM plugin or team-based coordination.
- Financial transaction systems: strong alignment for dual-approval.
- DocuSign: Fits contractual and critical document approval Use cases.
- Security incident platforms: Perfect match for automated actions that must be reviewed.

**Addresses:** [Excessive autonomy](threat-details.md#excessive-autonomy); [Goal Misalignment Cascades](threat-details.md#goal-misalignment-cascades); [Lateral Movement - Cross-Layer](threat-details.md#lateral-movement---cross-layer)

## Implement Just-In-Time and Just-Enough-Access controls

*Preventive*

Limit user access using Just-In-Time and Just-Enough-Access (JIT/JEA) principles. Grant access only for the necessary duration and with the minimum permissions required to complete specific tasks. Regularly review and adjust access rights to prevent unauthorized privilege escalation and reduce the risk of policy subversion and timing exploits.

**How to implement:**

- Integrate JIT/JEA with identity Management tools to automate temporary access provisioning.
- Define clear access policies for sensitive tasks and Enforce expiration on elevated privileges.
- Log and Monitor all privileged sessions for anomalies.
- regularly Audit access patterns to refine policies and ensure that permissions remain aligned with actual job functions and threat exposure.

**Why it works:** The implementation involves configuring access controls to ensure users receive permissions dynamically based on their needs. Access requests are evaluated in real-time, granting temporary permissions that expire after the task is completed. The system logs all access events and changes, with alerts for deviations from normal patterns. Anomaly detection algorithms monitor for timing discrepancies, while regular audits ensure compliance with JIT/JEA principles.

**Examples:**

- Microsoft Azure active Directory privileged identity Management (PIM) Enables just-in-time access to resources.
- AWS identity and access Management (IAM) allows for fine-grained access control, implementing temporary Security credentials for specific tasks.
- CyberArk Provides JIT access Management solutions that grant temporary privileges based on user roles and tasks.
- HashiCorp Vault can dynamically generate access credentials for applications, ensuring minimal access duration.

**Addresses:** [Lateral Movement - Cross-Layer](threat-details.md#lateral-movement---cross-layer); [Privilege Escalation](threat-details.md#privilege-escalation)

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

**Addresses:** [Server Side Request Forgery (SSRF)](threat-details.md#server-side-request-forgery-ssrf)

## Implement property-level access controls

*Preventive*

Implement access controls to restrict users from viewing or modifying object properties based on their authorization level.

**How to implement:**

- limit user access to Only the properties of objects they are authorized to view or modify
- Use a centralized access control mechanism to Enforce property-level rules consistently - regularly Audit access control logic to Identify misconfigurations or excessive privileges
- Log access to sensitive properties for traceability and incident response
- Train developers on secure handling of user permissions at the property level

**Why it works:** Property-level access controls ensure users can only view or modify specific object properties they are authorized to access. This is enforced through centralized authorization logic that checks user roles, attributes, or policies before granting access. Each sensitive property should have associated access rules. Logs of access attempts and regular audits help identify misconfigurations or over-permissive access. Developer training ensures secure implementation.

**Examples:**

- OAuth 2.0 scopes: Restrict access to specific user data fields
- AWS IAM Policies: Allow fine-grained access to object attributes
- RBAC in databases: Controls column-level access per role
- JWT claims: Carry property-level access rules for APIs
- ABAC: Enforces access using user and resource attributes
- Spring Security: Supports field-level restrictions in Java apps

**Addresses:** [Broken Object Property Level Authorization](threat-details.md#broken-object-property-level-authorization)

## Implement random and unpredictable record IDs

*Preventive*

Use random and unpredictable values, such as GUIDs, for record IDs to prevent unauthorized access.

**How to implement:**

- Use cryptographically secure random number generators to create record IDs (e.g., uuid V4)
- Avoid sequential or incremental IDs, which can be guessed or enumerated by attackers - ensure IDs are long enough to prevent brute-force Discovery - implement server-side ID generation to reduce exposure from client-controlled input
- Review and test ID generation mechanisms regularly to ensure randomness and resistance to prediction attacks

**Why it works:** Predictable record IDs (like auto-incrementing numbers) can expose APIs to enumeration and unauthorized access. To prevent this, IDs should be generated using cryptographically secure random number generators, such as UUID v4. These IDs should be long, unique, and generated server-side to prevent tampering or guessing. Regular reviews and tests of the ID generation process ensure continued resistance to prediction-based attacks.

**Examples:**

- uuid V4 libraries: generate secure, random identifiers using cryptographic RNGs
- Node.js uuid Package: Commonly used to generate unpredictable record IDs
- Firebase Firestore: Automatically Assigns non-sequential document IDs
- AWS DynamoDB: Supports random partition keys to Avoid predictable patterns
- OWASP ZAP: can be used to test for ID predictability or enumeration vulnerabilities
- Python secrets module: generates secure random strings for record IDs

**Addresses:** [Broken Object Level Authorization](threat-details.md#broken-object-level-authorization)

## Implement record-level authorization checks for all API endpoints

*Preventive*

Enforce record-level authorization checks for all API endpoints. Validate that the logged-in user has the necessary permissions for each record accessed based on client input in every relevant function.

**How to implement:**

- ensure robust authentication mechanisms are in place to verify user identity before authorization checks.
- Enforce record-level authorization in every API method accessing data
- Use role- or attribute-based access control to simplify permission logic - conduct Security testing to Validate that authorization logic cannot be bypassed

**Why it works:** Record-level authorization ensures users access only data they are permitted to see. API methods must include explicit checks verifying the user’s identity and permissions for each record accessed. Role- or attribute-based access control can help manage these permissions efficiently. Security testing, including authorization bypass tests, is essential to verify that unauthorized users cannot access or manipulate protected data.

**Examples:**

- OAuth 2.0: Supports fine-grained scopes for user-specific API access
- AWS IAM: Applies user roles to restrict access to specific resources
- Firebase Security Rules: Enforces user- and attribute-based access at the data level
- Spring Security: Supports method- and object-level authorization logic
- Auth0: Implements RBAC and ABAC for record-based access decisions
- Casbin: A lightweight policy engine supporting per-record access enforcement

**Addresses:** [Broken Object Level Authorization](threat-details.md#broken-object-level-authorization)

## Implement resource limits

*Preventive*

Set strict limits on memory, CPU, and file descriptors for applications to prevent resource exhaustion. Use technologies such as containers or serverless architectures to enforce these limits effectively.

**How to implement:**

- regularly Review and adjust resource limits based on usage trends
- Monitor CPU, memory, and I/O to detect spikes or abuse
- Configure alerts when usage nears set thresholds
- Use request-based rate limiting to prevent resource exhaustion
- Log and analyze resource usage for abnormal patterns
- Simulate attacks to test how well limits prevent denial of Service

**Why it works:** Resource limits prevent a single process or user from consuming excessive memory, CPU, or I/O. Containers and serverless platforms can enforce these limits automatically. Administrators should monitor usage in real time and set alerts when thresholds are exceeded. Logging and testing help detect resource abuse and validate the effectiveness of limits. Rate limiting can be added to control incoming request volume and reduce the risk of overload.

**Examples:**

- Kubernetes: Enforces memory and CPU limits per container
- AWS Lambda: Applies time and memory constraints by default
- Docker: Supports CPU/memory limits on individual containers
- Google cloud Run: Automatically scales with resource limits
- Prometheus: Tracks resource usage and triggers alerts
- Systemd resource controls: Restrict CPU, I/O, and memory at the OS level

**Addresses:** [Denial of Service (DoS) Attacks - AI infrastructure](threat-details.md#denial-of-service-dos-attacks---ai-infrastructure); [Resource Hijacking](threat-details.md#resource-hijacking); [Unrestricted Resource Consumption](threat-details.md#unrestricted-resource-consumption)

## Implement robust sandboxing measures

*Preventive*

Implement sandboxing to isolate the training environment and prevent unauthorized data access or manipulation. Enforce strong access controls and validate training data to ensure integrity and accuracy.

**How to implement:**

- Utilize containerization technologies to create isolated environments for training processes.
- implement strict access controls and authentication mechanisms for data input sources.
- Employ monitoring to detect unauthorized activity during training.
- Integrate automated data validation tools to flag suspicious or inconsistent data entries.
- regularly update and patch sandboxing tools.
- conduct threat modeling to Identify potential attack vectors specific to the training environment.

**Why it works:** Sandboxing isolates the training process using containers and strict access controls. Real-time monitoring and automated validation help detect and block anomalies. Updates and threat modeling improve system resilience

**Examples:**

- Docker and Kubernetes for creating isolated training environments.
- Apache Kafka for managing data streams with strict access controls.
- SELinux or AppArmor for enforcing Security policies on training processes.
- Snort or Suricata for Real-time monitoring of network traffic for anomalies.
- TensorFlow data validation for automated data validation and integrity checks.
- Git for version control of training data to track changes and Identify malicious alterations.

**Addresses:** [Data Exfiltration](threat-details.md#data-exfiltration); [Data Poisoning - AI Agent](threat-details.md#data-poisoning---ai-agent); [Inject malicious stuff into training process](threat-details.md#inject-malicious-stuff-into-training-process); [Malicious pre-training](threat-details.md#malicious-pre-training); [Security Agent Data Poisoning](threat-details.md#security-agent-data-poisoning)

## Implement Role-Based Access Control (RBAC)

*Preventive*

Restrict system access by assigning permissions based on user or service roles. RBAC ensures that users, applications, or LLMs can only access resources necessary for their role, minimizing the risk of unauthorized actions. Define roles with clear scopes, assign them to entities based on operational needs.

**How to implement:**

- Identify all user and Service roles based on operational needs.
- Define permissions clearly for each role and follow the principle of least privilege when assigning permissions.
- implement a robust onboarding and offboarding process to manage role assignments.
- Monitor access patterns to detect misuse or privilege escalation.
- regularly Review and update roles to reflect changes in responsibilities or system architecture.

**Why it works:** RBAC implementation involves defining distinct user roles with specific permissions aligned to job functions. Access control decisions are made based on these roles, ensuring users only access resources necessary for their duties. Authorization checks are enforced at all entry points, validating user roles against requested actions. Regular audits and monitoring track role assignments, while automated tools assist in detecting anomalies and ensuring compliance with least privilege principles.

**Examples:**

- Examples of technology that implement RBAC include:
- Microsoft Azure Active Directory
- AWS Identity and Access Management (IAM)
- Okta, and Google Cloud Identity.
- Tools like HashiCorp Vault and Kubernetes RBAC can enforce role-based permissions.
- Security Information and Event Management (SIEM) solutions, such as Splunk and IBM QRadar, can monitor and audit role assignments and access patterns to ensure compliance with least privilege principles.

**Addresses:** [Elevation of Privilege](threat-details.md#elevation-of-privilege); [Membership Inference Attacks](threat-details.md#membership-inference-attacks); [Model theft](threat-details.md#model-theft)

## Implement schema-based response validation

*Preventive*

Enforce schema-based response validation for all API methods to ensure only authorized object properties are returned, preventing unauthorized access to sensitive data.

**How to implement:**

- Define strict response schemas for each API to limit exposed fields
- Validate responses before sending them to users using Schema rules - update schemas regularly to reflect changes in data sensitivity or access rules
- Enforce Schema-level validation errors to prevent fallback to full object exposure - handle errors securely to Avoid leaking sensitive info
- Monitor response validation failures and investigate anomalies

**Why it works:** Schema-based response validation ensures only approved fields are returned by the API. JSON or XML schemas define allowed properties for each endpoint and user context. Responses are validated before being sent to the client, blocking unintended data exposure. Validation failures must be logged and investigated. Error messages should be generic to prevent information leakage. Schema reviews ensure alignment with security and data classification policies.

**Examples:**

- GraphQL schemas: Restrict returned fields based on roles and queries
- Ajv / Joi: JavaScript libraries for validating JSON responses against schemas
- AWS API gateway: Enforces Schema validation for rest APIs
- OpenAPI / Swagger: Supports response Schema definitions and validation
- Apigee: Provides Schema enforcement and response inspection features
- Zally: Enforces Schema rules in OpenAPI contracts during CI/CD

**Addresses:** [Broken Object Property Level Authorization](threat-details.md#broken-object-property-level-authorization); [Data Leakage](threat-details.md#data-leakage)

## Implement secondary review for uploaded artifacts

*Detective*

Require a secondary review and approval process for all uploaded artifacts (e.g., files, code, packages), ensuring each artifact is verified by a designated reviewer before being used in production or internal environments.

**How to implement:**

- Establish clear criteria for what constitutes a reviewable artifact.
- Designate reviewers with appropriate expertise and authority.
- implement automated tools to assist in the Review process.
- Maintain an Audit trail of all reviews and approvals.
- set time limits for the Review process to prevent delays.
- Train reviewers on identifying potential Security threats.
- regularly update Review criteria based on emerging threats.

**Why it works:** Artifacts from other accounts, especially in shared or multi-tenant setups, can introduce malicious code, backdoors, or misconfigurations. Without proper review, these artifacts may bypass security checks and be deployed internally or to production. A secondary review process ensures artifacts are scanned, verified, and approved before use, reducing risk and enhancing supply chain security.

**Examples:**

- GitHub actions for automated workflows that Enforce Review processes on pull requests and artifact uploads.
- JFrog Artifactory with built-in approval workflows for artifact promotion.
- Azure DevOps with gated Check-ins that Require approvals before deployment.
- Jenkins with plugins for manual approvals and Review gates on pipeline stages.
- Sonatype Nexus repository with policies for promoting artifacts based on Security Scans and reviews.

**Addresses:** [Backdoor Attacks - AI framework](threat-details.md#backdoor-attacks---ai-framework); [Backdoor Attacks - AI model](threat-details.md#backdoor-attacks---ai-model); [Compromised Framework Components](threat-details.md#compromised-framework-components); [Supply Chain Attacks](threat-details.md#supply-chain-attacks); [Supply Chain Attacks - Cross-Layer](threat-details.md#supply-chain-attacks---cross-layer)

## Implement strict compartmentalization of safe areas

*Preventive*

Establish strict compartmentalization by defining "safe" areas with clear trust boundaries. Prevent sensitive data from leaving these boundaries and exercise caution when interacting with external compartments. Integrate compartmentalization into system design, ensuring it supports privilege separation. Apply the principle of least privilege to determine when to use or drop privileges.

**How to implement:**

- Define safe areas with strict access controls and boundaries.
- Use automated tools to detect permission misconfigurations.
- assign permissions based on roles using ACLs or RBAC.
- Train staff on privilege separation and compartmentalization.
- Monitor access and Audit safe areas for unauthorized modifications.
- limit software in safe areas to essential components only.

**Why it works:** Design implementation separates the system into compartments with defined boundaries and restricted access. Role-based controls ensure only authorized users access specific zones. Automation checks permissions and prevents misconfigurations. This reduces exposure risk and supports least-privilege enforcement.

**Examples:**

- SELinux: Applies mandatory access control to Enforce safe area boundaries.
- AppArmor: limits application behavior based on Security profiles.
- Windows UAC: Enforces elevation prompts for protected actions.
- Docker: containers isolate workloads for safer execution.
- Kubernetes RBAC: controls access to pods and services.

**Addresses:** [Data Exfiltration](threat-details.md#data-exfiltration); [Lateral Movement - AI infrastructure](threat-details.md#lateral-movement---ai-infrastructure)

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

**Addresses:** [Broken Authentication](threat-details.md#broken-authentication); [Repudiation](threat-details.md#repudiation); [Spoofing](threat-details.md#spoofing)

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

**Addresses:** [Supply Chain LLM Issues](threat-details.md#supply-chain-llm-issues)

## Implement Trust Boundaries for LLM Interactions

*Preventive*

Establish strict trust boundaries for LLM interactions. Treat the LLM as untrusted; ensure users retain control over decisions. Limit external sources and extensible functionalities, such as plugins, to minimize risk. Regularly review and update security measures to address potential vulnerabilities and ensure user data protection.

**How to implement:**

- clearly Define the boundary between trusted and untrusted components when integrating LLMs.
- sanitize all inputs and outputs to prevent injection or data leakage.
- Restrict LLM access to sensitive functions and external systems.
- Disable unneeded plugins or APIs.
- regularly assess extensions and dependencies for Security risks.
- Log interactions and Review them to detect unsafe behavior or drift from intended Use
- Educate users on the LLM risks and the importance of skepticism.

**Why it works:** Design implementation involves creating a layered architecture where the LLM operates in a sandboxed environment, isolating it from direct access to user data and external systems. System operational mechanics include real-time input validation and content filtering at the API level, enforcing role-based access controls, and maintaining comprehensive logging for all interactions.

**Examples:**

- API Gateways like AWS API gateway, Kong, to control access and Validate inputs
- Sanitization tools like DOMPurify, AntiXSS to clean prompts and responses
- Moderation APIs like OpenAI Moderation, Azure Content Safety, to filter harmful Content - containers like Docker, Firecracker to isolate LLM processes - access control tools like OPA, Auth0 to Enforce permissions - monitoring tools like Splunk, Datadog to track interactions - plugin controls. whitelist Only trusted plugins

**Addresses:** [Direct prompt injection](threat-details.md#direct-prompt-injection); [Indirect prompt injection](threat-details.md#indirect-prompt-injection); [Membership Inference Attacks](threat-details.md#membership-inference-attacks); [Model Stealing](threat-details.md#model-stealing); [Reprogramming Attacks](threat-details.md#reprogramming-attacks); [Rogue LLM Instructions](threat-details.md#rogue-llm-instructions); [User-driven prompt injection](threat-details.md#user-driven-prompt-injection)

## Implement URL Validation with Allowlists

*Preventive*

Implement allowlists for remote origins, URL schemes, ports, and accepted media types to prevent unauthorized requests and mitigate SSRF risks.

**How to implement:**

- regularly update the allowlist to reflect current trusted services and Remove deprecated entries.
- Use strict pattern matching to Validate URLs, including regex checks for structure and allowed characters.
- implement logging and monitoring for any requests that are denied due to allowlist violations.

**Why it works:** The implementation involves defining a strict allowlist that specifies permitted URL patterns, schemes (e.g., HTTP, HTTPS), and ports. Each incoming request is validated against this allowlist using regex for structural integrity and allowed characters. Denied requests trigger logging for audit and monitoring purposes. The system employs real-time checks to ensure compliance with the allowlist, and updates are scheduled to reflect any changes in trusted services.

**Examples:**

- AWS Lambda with API gateway: for domain restriction
- NGINX: with rewrite rules for allowlist enforcement
- ModSecurity: WAF to block unlisted URLs

**Addresses:** [Server Side Request Forgery (SSRF)](threat-details.md#server-side-request-forgery-ssrf)

## Implement user approval for privileged actions

*Preventive*

Require explicit user approval for all privileged actions, such as sending or deleting emails, to prevent unauthorized operations resulting from prompt injections or other attacks. This ensures that users are aware of and consent to significant actions taken by the application.

**How to implement:**

- Define which actions Require explicit user approval
- Design approval prompts that clearly state the action and its impact - limit automated triggers to non-privileged operations - ensure approvals are time-bound and Require re-verification if expired
- Send users confirmation alerts and Maintain Audit logs of approvals

**Why it works:** User approval ensures high-risk actions, like sending messages or modifying data, can’t proceed without explicit user consent. The system should display a clear prompt for confirmation and restrict LLM- or app-initiated privileged actions. Expired approvals should require re-verification. Logs and notifications promote transparency and accountability.

**Examples:**

- Zapier / Power automate: Require user approval before executing high-risk tasks in workflows
- GitHub environments: Enforce manual approval before deploying to production
- Google Workspace Admin actions: Prompt admins to confirm actions like user deletion or data export
- AWS IAM access Analyzer / Change Manager: request and Log approval for high-impact infrastructure changes
- Custom in-app prompts: Designed within the app UI to pause privileged actions until users confirm intent

**Addresses:** [Direct prompt injection](threat-details.md#direct-prompt-injection); [Excessive autonomy](threat-details.md#excessive-autonomy); [Indirect prompt injection](threat-details.md#indirect-prompt-injection); [Rogue LLM Instructions](threat-details.md#rogue-llm-instructions); [User-driven prompt injection](threat-details.md#user-driven-prompt-injection)

## Implement user tracking for minimum permission enforcement

*Detective*

Enforce minimum permissions by tracking user authorization and ensuring that actions on downstream systems are executed with only the necessary privileges for each user.

**How to implement:**

- regularly Review and Audit user permissions to Identify and Remove excessive access.
- implement role-based access control (RBAC) to streamline permission assignments.
- Use automated tools to Monitor and alert on permission changes or anomalies.
- Establish clear policies for permission requests and approvals.
- Provide training for users on the importance of least privilege access.
- ensure logging of user actions to facilitate accountability and forensic analysis.

**Why it works:** User tracking for minimum permission enforcement involves implementing a system that logs user actions and access requests in real-time. Each action is validated against a predefined set of permissions based on user roles. When a user attempts to access a resource, the system checks their current permissions against the required permissions for that action. If the permissions exceed the minimum required, the action is denied.

**Examples:**

- AWS IAM allows for fine-grained access control and the implementation of least privilege by defining roles and permissions for users and services.
- Azure active Directory Provides RBAC to manage user permissions and track access across various Azure resources.
- Okta identity cloud Offers user tracking and permission Management features.
- Google cloud IAM Enables users to Define roles and permissions, ensuring that users Have Only the access they need for their tasks.

**Addresses:** [Lateral Movement - Cross-Layer](threat-details.md#lateral-movement---cross-layer)

## Implement User-Supplied Info in Vector Database

*Preventive*

Utilize a vector database to integrate user-supplied information while enforcing validation and sanitization. This enables secure incorporation of real-time updates without retraining the model and protects against data poisoning or injection attacks.

**How to implement:**

- Validate and sanitize all user-submitted data before it is stored in the vector database.
- Use anomaly detection to flag suspicious patterns in user-submitted content.
- conduct regular audits of vector database entries specifically sourced from user input.
- track changes through versioning to roll back malicious user data if needed.
- Enable a feedback mechanism for users to report unsafe or inaccurate content.

**Why it works:** Secure ingestion of user-generated information in vector databases ensures that all user-supplied data undergo validation and sanitization before storage. Version control enables rollbacks when unsafe data is identified, and audit logs support traceability. A user feedback loop empowers quick responses to potentially malicious contributions, helping maintain system reliability without full model retraining.

**Examples:**

- Pinecone, Weaviate, and Milvus support user-supplied input with vector updates and integrated validation features.
- Elasticsearch can Monitor Real-time user input and alert on malicious contributions.
- TensorFlow data validation can be used to Check the integrity of user-submitted vector entries.
- versioning tools and rollback features in these platforms help revert poisoned vectors without disrupting service.

**Addresses:** [Inject malicious stuff into training process](threat-details.md#inject-malicious-stuff-into-training-process); [Malicious pre-training](threat-details.md#malicious-pre-training)

## Instruction Isolation with Guardrail Mediation Layer

*Preventive*

Separate user content from system and tool instructions, and route all LLM-generated tool calls through a guardrail or policy engine that inspects intent, filters unsafe actions, and rejects tool invocations that originate from or are influenced by untrusted prompt content.

**Addresses:** [LLM Chain Injection](threat-details.md#llm-chain-injection)

## Isolate resource fetching mechanisms within the network.

*Preventive*

Isolate resource fetching mechanisms to restrict access to internal services. Implement strict network segmentation and ensure that APIs can only access necessary external resources. Use firewalls to block unauthorized requests and validate all incoming data to prevent SSRF attacks.

**How to implement:**

- limit API access with least privilege to control what services they can call.
- Review and Enforce network segmentation regularly to prevent access to internal services.
- Use WAFs and proxies to detect SSRF and filter outbound requests.
- Log all outbound traffic and Audit anomalies.
- Validate URLs and sanitize input to reduce SSRF risk.

**Why it works:** APIs should run in isolated network segments with controlled outbound access. Configure firewall rules and proxies to allow only specific, approved external endpoints. Use Web Application Firewalls (WAFs) to detect Server-Side Request Forgery (SSRF) attempts and log all outbound requests for auditing. Apply input validation to block untrusted URLs. Regular audits help ensure that segmentation and access restrictions remain effective.

**Examples:**

- AWS VPC endpoints allow private connections between VPC and AWS services without public/internet exposure
- Azure private Link Enables private access to Azure services over isolated endpoints
- Google cloud VPC Service controls defines secure perimeters to prevent data exfiltration through unauthorized resource access
- NGINX strict routing Restricts outbound traffic to approved domains Only
- Istio Service mesh Enforces fine-grained, Policy-based communication rules for internal API calls

**Addresses:** [Denial of Service (DoS) Attacks - AI infrastructure](threat-details.md#denial-of-service-dos-attacks---ai-infrastructure); [Resource Hijacking](threat-details.md#resource-hijacking); [Server Side Request Forgery (SSRF)](threat-details.md#server-side-request-forgery-ssrf)

## Limit LLM Plugin Functions

*Preventive*

Restrict LLM plugins to only essential functions to minimize potential attack vectors.

**How to implement:**

- conduct a thorough Audit of all available plugin functions to Identify and eliminate unnecessary ones.
- implement role-based access controls to Restrict function usage based on user roles.
- regularly Review and update the list of permitted functions as system requirements evolve.
- Monitor and Log plugin usage to detect any unauthorized access attempts or unusual behavior.
- Provide training for users on the importance of using Only necessary functions to enhance Security awareness.

**Why it works:** This control limits plugin functionality through whitelisting, allowing only necessary operations per user role. Role-based permissions enforce access restrictions, while logging systems track usage to flag unusual activity. Regular audits ensure the whitelist stays current. Training reinforces secure use of minimal plugin capabilities.

**Examples:**

- AWS IAM and Azure active Directory: Enforce role-based access to plugin functions.
- Kubernetes: Restrict plugin communication through network policies.
- containerization platforms: limit exposure via isolated environments.
- API Gateways: Apply strict access policies.
- SIEM tools (e.g., Splunk): Monitor and Log plugin function usage

**Addresses:** [Denial of Service (DoS) Attacks - AI model](threat-details.md#denial-of-service-dos-attacks---ai-model); [Excessive functionality](threat-details.md#excessive-functionality); [Model Stealing](threat-details.md#model-stealing)

## Limit parameter and payload sizes

*Preventive*

Define and enforce maximum limits on all incoming parameters and payload sizes to prevent resource exhaustion and mitigate potential DoS attacks.

**How to implement:**

- Define input size limits for body, headers, and query parameters
- Validate request size server-side before processing
- Reject oversized inputs with proper HTTP error codes
- Log and Monitor size-limit violations for analysis
- Tune limits over time based on observed usage and threat patterns
- Use WAFs or Middleware to Enforce limits as close to entry as possible

**Why it works:** Size-based attacks can exhaust memory or processing resources. To prevent this, configure server or middleware components to reject inputs that exceed defined limits for body, query, or headers. Requests over the threshold should return errors like HTTP 413. Logging should track repeated violations for analysis. Periodic review of usage trends and threat intelligence helps ensure that the defined limits remain appropriate and effective.

**Examples:**

- AWS WAF / Cloudflare WAF: block requests exceeding size thresholds
- NGINX / HAProxy: Configure max body and header sizes
- Kong / Apigee: API Gateways with request size enforcement
- Express.js / Django: Use Middleware to limit and Validate input sizes
- Spring Boot: Supports multipart and payload size limits via config
- FastAPI / Flask: allow Custom validation logic for payload constraints

**Addresses:** [Unrestricted Resource Consumption](threat-details.md#unrestricted-resource-consumption)

## Limit plugin functionality

*Preventive*

Restrict plugin functionality to essential features only. Eliminate open-ended functions like shell commands or URL fetching. Choose plugins and tools that offer specific, limited capabilities to minimize potential attack vectors.

**How to implement:**

- Audit plugins and Enforce access controls to ensure Only necessary, low-risk features are enabled.
- regularly Review and update plugins to ensure they adhere to the principle of least privilege.
- Monitor plugin usage for unusual activity that may indicate exploitation attempts.

**Why it works:** Limit plugin functionality by enforcing a whitelist that only permits narrowly scoped plugins necessary for task execution. Combine role-based access with continuous monitoring of plugin activity and interactions. Real-time logging and anomaly detection help detect misuse, while regular reviews ensure only approved capabilities remain enabled.

**Examples:**

- OpenAI plugin Manifest Scopes: Enforces strict access declarations to limit plugin functionality.
- AWS Lambda: allows Execution of tightly scoped serverless functions, reducing attack surface.
- Kubernetes RBAC: Restricts plugin and API access based on user roles and least privilege.
- Helicone: Monitors plugin calls and usage in OpenAI environments for Security compliance.

**Addresses:** [Excessive functionality](threat-details.md#excessive-functionality)

## Limit property exposure

*Preventive*

Limit property exposure by implementing fine-grained access controls. Ensure that only authorized users can access sensitive object properties. Replace automatic object serialization or default field exposure with explicit selection of properties to include in API responses, views, or outputs. This reduces the risk of unintentionally leaking sensitive data.

**How to implement:**

- Avoid exposing object properties by default; expose only what's necessary
- Replace generic serialization with explicitly defined fields for output
- Remove sensitive or unused properties from API responses and UI layers
- Use data transformation layers (e.g., DTOs or serializers) to control exposure
- Review property exposure across endpoints and adjust based on role and context
- Train developers to recognize overexposure risks in APIs and object mappings

**Why it works:** Limiting property exposure means explicitly defining which object fields are returned to users instead of relying on default serialization. Automatically exposing entire objects can leak sensitive data. Use DTOs, serializers, or view models to control what properties are included. Tailor responses to the user's role or context, and audit API outputs to catch overexposed fields. This reduces the risk of data leakage and supports the principle of least privilege.

**Examples:**

- Spring Boot DTOs: expose Only selected fields in API responses
- Django rest framework serializers: control which fields appear in responses
- GraphQL resolvers: Return Only authorized fields per query context
- TypeScript interfaces or class transformers: Shape exposed objects explicitly
- Express.js with manual res.json(): Select which fields to Include in outputs
- Postman or Burp Suite: used to Audit and detect overexposed fields

**Addresses:** [Broken Object Property Level Authorization](threat-details.md#broken-object-property-level-authorization); [Data Leakage](threat-details.md#data-leakage)

## Limit resource usage per request.

*Preventive*

Implement a limit on resource usage for each request to prevent excessive task generation. Set thresholds that slow down or block requests that exceed defined resource limits.

**How to implement:**

- Establish clear thresholds based on historical usage patterns to optimize limits.
- implement dynamic scaling to adjust limits based on system load.
- Use rate limiting to control the frequency of requests from individual users.
- Monitor and Log usage patterns to Identify potential abuse.
- Provide feedback to users when limits are reached to improve user experience.
- Consider implementing a cooldown period after reaching limits to prevent rapid retries.

**Why it works:** Design implementation involves setting fixed thresholds for CPU, memory, and queue length per request. Utilize a middleware layer to intercept incoming requests and measure resource consumption against these thresholds. If limits are exceeded, apply throttling or reject the request. Operational mechanics include continuous monitoring of resource usage, adjusting thresholds dynamically based on current load, and logging all requests to analyze patterns for future adjustments.

**Examples:**

- Examples of technology that implements resource usage limits include:
- AWS API Gateway and Azure API Management for per-request throttling.
- NGINX and HAProxy for connection limits.
- Google Cloud Functions to limit memory/time per function.
- Redis for managing request queues.

**Addresses:** [Denial of Service (DoS) Attacks - AI infrastructure](threat-details.md#denial-of-service-dos-attacks---ai-infrastructure); [LLM Denial of Service](threat-details.md#llm-denial-of-service); [Resource Hijacking](threat-details.md#resource-hijacking)

## Linked Deletion Workflows for Source and Embeddings

*Corrective*

Tie each embedding to a unique source record ID and enforce deletion workflows that cascade from the source-of-truth system to the vector index, ensuring embeddings are hard-deleted or tombstoned whenever the original document is removed or access is revoked.

**Addresses:** [Improper Data Retention / Deletion](threat-details.md#improper-data-retention--deletion)

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

## Make agent identity visible and verifiable

*Preventive*

Ensure AI agents present clear, verifiable identity details to users and other agents, making impersonation significantly harder.

**How to implement:**

- Provide strong identity markers. Use unique IDs, cryptographic certificates, and visual trust badges to prevent spoofing.
- Enforce consistent identity presentation. standardize how identity (origin, owner, purpose) is shown in interfaces and APIs so attackers cannot exploit inconsistencies.
- Integrate reputation and certification. Maintain visible reputation scores or certifications tied to compliance frameworks (EU AI Act, NIST AI RMF, OECD AI principles) to distinguish trusted agents.

**Why it works:** Transparent identity reduces the success of impersonation by giving users and systems clear trust cues. This is achieved by combining unique identifiers, tamper-proof credentials, and visible trust indicators so that impersonators cannot easily pass as legitimate agents.

**Examples:**

- Agents display their verified certificate chain, organization, and role alongside a trust indicator (similar to HTTPS lock icons). Additional reputation scores and conformity badges (e.g., EU AI Act "high-risk compliant") provide ongoing verification.

**Addresses:** [Agent Impersonation](threat-details.md#agent-impersonation)

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

## Map industry regulations to AI agent design

*Preventive*

Developers must identify and implement security and compliance requirements from relevant industry standards (e.g., HIPAA for healthcare, PCI DSS for finance, GDPR for privacy, EU AI Act for high-risk AI) into the design of AI agents.

**How to implement:**

- Identify applicable regulations: Determine which laws, regulations, or standards Apply to the AI agent’s industry or Use case.
- Integrate compliance into architecture: Embed controls like encryption, access restrictions, and data minimization at Design time rather than as afterthoughts.
- Align with regulatory audits: Design systems so compliance evidence (e.g., Audit logs, certifications) can be easily generated and reviewed

**Why it works:** Generic security is not enough for vertical AI solutions. Domain-specific vulnerabilities can be exploited if industry standards and workflows are not integrated into design and testing. Industry-specific regulations establish baseline protections that AI agents must follow. Incorporating these early in design ensures the solution is compliant, reduces risk of violations, and prevents systemic exploitation of sector-specific weaknesses.

**Examples:**

- A healthcare AI agent handling patient records integrates HIPAA controls: encrypts PHI in transit and at rest, applies role-based access controls, and logs all access attempts for compliance audits.

**Addresses:** [Horizontal/Vertical Solution Vulnerabilities](threat-details.md#horizontalvertical-solution-vulnerabilities)

## Monitor LLM resource utilization for anomalies

*Detective*

Continuously track LLM resource usage to detect unusual spikes or patterns that could signal a DoS attack.

**How to implement:**

- Define baseline metrics for CPU, memory, and network usage.
- Configure Real-time alerts to flag unusual usage spikes.
- Integrate machine learning for anomaly detection accuracy.
- regularly update alert thresholds based on historical usage.
- Enable centralized logging for resource utilization.
- Link alerting to incident response workflows for rapid containment.

**Why it works:** A monitoring system collects LLM resource usage data at intervals and stores it in a centralized log. Statistical models and ML algorithms analyze this data to detect abnormal patterns. When thresholds are exceeded, alerts are triggered, initiating predefined incident response actions.

**Examples:**

- Prometheus + Grafana: For collecting and visualizing resource metrics like CPU and memory
- Datadog: Provides anomaly detection and usage monitoring across cloud environments
- AWS CloudWatch: Tracks resource usage
- Weights & Biases (W&B): Monitors LLM training and inference metrics including GPU usage and token count
- Arize AI: Tracks LLM performance, embedding drift, and feedback signals
- Helicone: Specialized monitoring for OpenAI APIs, including latency and usage spikes

**Addresses:** [Denial of Service (DoS) Attacks - AI infrastructure](threat-details.md#denial-of-service-dos-attacks---ai-infrastructure); [Denial of Service (DoS) Attacks - AI model](threat-details.md#denial-of-service-dos-attacks---ai-model); [Resource Hijacking](threat-details.md#resource-hijacking)

## Monitor production code for drift

*Detective*

Continuously monitor production code for discrepancies with CI/CD sources. Implement automated alerts for unauthorized changes and establish a process for rapid remediation of any detected drift.

**How to implement:**

- Use digital signatures to verify the integrity and authenticity of artifacts before deployment.
- conduct regular Security audits of the CI/CD pipeline to Identify vulnerabilities.
- Employ automated vulnerability scanning tools on all deployed artifacts.
- Establish a rollback mechanism to quickly revert to a previous state in case of detected malicious activity.

**Why it works:** The system continuously compares the current state of production code against the defined state in CI/CD repositories. Automated tools scan for unauthorized changes and discrepancies, triggering alerts for investigation. A dashboard displays drift instances, while a remediation workflow facilitates quick responses. Regular validation processes ensure compliance with security standards, and logs maintain an audit trail for accountability and further analysis.

**Examples:**

- ArgoCD / Flux: Monitor and Enforce Git-based deployment states
- Chef InSpec / Terraform compliance: detect drift in infrastructure config
- Prometheus & Grafana: alert on production state anomalies
- Aqua Security / Twistlock: Monitor deployed containers for unexpected changes

**Addresses:** [Compromised Container Images](threat-details.md#compromised-container-images)

## Network Egress Control and Data Minimization for Retriever Components

*Preventive*

Run retriever services in locked-down network segments with strict egress controls and minimal outbound destinations, while limiting the amount and sensitivity of data passed into the retriever, so even a poisoned library cannot send retrieval contents to unapproved endpoints.

**Addresses:** [RAG Supply Chain Poisoning](threat-details.md#rag-supply-chain-poisoning)

## Neutralize and contain backdoors during deployment and runtime

*Corrective*

Apply remediation techniques and runtime safeguards to neutralize backdoors that survived earlier stages and contain novel triggers discovered in production. This ensures that even if hidden behaviors are activated, such as a special token, a trigger phrase in a prompt, or a watermarked image, they cannot cause unsafe or malicious outcomes in live systems.

**How to implement:**

- Runtime detection: Apply STRIP entropy tests, self-consistency checks, and ensemble verification to identify invariant trigger behavior in production.
- Alignment gates: Route suspicious outputs through verification gates for blocking, sanitization, or human-in-the-loop escalation (refer to 'Establish alignment verification gates for agent outputs' mitigation).
- Containment testing: Use sandboxed execution to simulate trigger propagation and assess ecosystem-level blast radius.
- Recovery & rollback: Enable kill switches to disable compromised models; document remediation steps in backdoor test reports.

**Why it works:** Even with rigorous training-time defenses, backdoors may survive or emerge at runtime. By combining neutralization techniques with runtime detection and containment, organizations ensure that hidden triggers cannot escalate into production-level failures. Alignment gates and sandbox testing limit blast radius, while rollback mechanisms provide resilience and fast recovery from newly discovered backdoors.

**Examples:**

- Neutralization: Fine-pruning pipelines in PyTorch or TensorFlow; defensive distillation methods.
- Runtime detection: STRIP (Strong Intentional Perturbation), ensemble-based anomaly detection, self-consistency checks.
- Containment: Istio EnvoyFilter or Kong Gateway for gating suspicious outputs; sandbox testing with Kubernetes namespaces.
- Recovery: AWS CloudWatch alarms tied to kill switch automation, SIEM/SOAR workflows for incident response.

**Addresses:** [Backdoor Attacks - AI model](threat-details.md#backdoor-attacks---ai-model)

## Perform domain-specific threat modeling for AI agents

*Preventive*

Developers must conduct tailored threat modeling to identify risks unique to the AI agent’s industry or function, ensuring that domain-specific attack surfaces and abuse cases are considered during development.

**How to implement:**

- Identify domain workflows: Map how the AI agent is used in its sector (e.g., patient intake, financial transactions).
- Model sector-specific threats: Consider attacks unique to the domain, such as patient data leakage in healthcare or insider trading in finance.
- Leverage frameworks: Use STRIDE, MITRE ATLAS, or OWASP AI Security guidance, but adapt scenarios to industry-specific workflows.

**Why it works:** Generic threat models miss vertical risks. By focusing on domain workflows and compliance environments, developers can anticipate and mitigate attacks that exploit industry-specific weaknesses.

**Examples:**

- A financial AI agent undergoes threat modeling where scenarios include fraudulent trade execution, unauthorized portfolio manipulation, and conflicts with SEC regulations. Mitigations like transaction limits and anomaly detection are built in

**Addresses:** [Horizontal/Vertical Solution Vulnerabilities](threat-details.md#horizontalvertical-solution-vulnerabilities); [Supply Chain Attacks - Cross-Layer](threat-details.md#supply-chain-attacks---cross-layer)

## Physically and Logically Isolated Tenant Indexes

*Preventive*

Use per-tenant vector indexes or strongly isolated namespaces with enforced tenant IDs at the storage layer, ensuring each request is cryptographically authenticated and authorized against its tenant boundary before any read or write is allowed.

**Addresses:** [Tenant Boundary Violation](threat-details.md#tenant-boundary-violation)

## Prevent misuse of tools by AI agents

*Preventive*

Tools are external functions or integrations that AI agents can invoke to perform actions, such as APIs, plugins, system commands, or service connectors. Prevent misuse by ensuring these tools are only used in intended, safe ways with constraints and validation.Ensure AI agents only use tools in intended, safe ways, with constraints and validation to prevent harmful or unforeseen actions.

**How to implement:**

- Restrict tool permissions. Do not give agents broad or unnecessary access. Bind tools to specific roles or contexts with explicit allow-lists.
- Validate tool inputs and outputs. Add input Sanitization and output checks to prevent unsafe tool execution. for sensitive tools, Require human approval.
- Enforce guardrails on chaining. prevent agents from combining multiple tools in ways that bypass safeguards. Use Policy engines or Execution sandboxes to Enforce limits.

**Why it works:** Agents often misuse tools when too much autonomy is granted or when integrations lack guardrails. Preventing misuse involves limiting scope, validating use, and enforcing context-specific policies so tools are invoked only in safe and intended ways.

**Examples:**

- A finance assistant agent can access an API to check balances but cannot execute payments unless a human approves. Tool inputs are validated to reject malformed or malicious requests, and all invocations are logged and rate-limited.

**Addresses:** [Agent Tool Misuse](threat-details.md#agent-tool-misuse)

## Prevent overfitting and memorization during training

*Preventive*

Reduce the risk of membership inference and similar privacy attacks by ensuring models do not memorize or overfit on specific training records. Apply differential privacy, regularization, and controlled training practices to strengthen generalization and protect confidentiality.

**How to implement:**

- Use DP-SGD or similar methods to add calibrated noise to gradients, making it mathematically hard to infer whether a specific record was in training.
- Apply dropout, weight clipping, weight decay, and other techniques to reduce memorization of individual samples.
- Monitor training/validation loss divergence and halt training before overfitting occurs.
- Remove or anonymize personally identifiable information (PII) where possible, and partition sensitive datasets carefully.
- Run membership inference probes (shadow models, confidence-based attacks) during validation to evaluate leakage risk.

**Why it works:** Overfitting increases the likelihood that a model memorizes details from training data, which attackers can exploit to infer membership. By introducing noise, applying regularization, and validating with privacy-focused tests, organizations can train models that generalize better and minimize privacy leakage risks.

**Examples:**

- Differential privacy: TensorFlow Privacy, PyTorch Opacus (DP-SGD).
- Regularization: Built-in dropout layers and weight decay in TensorFlow, PyTorch, or Keras.
- Early stopping: Keras callbacks, scikit-learn early_stopping_rounds.
- Adversarial evaluation: ML Privacy Meter for membership inference risk measurement.

**Addresses:** [Membership Inference Attacks](threat-details.md#membership-inference-attacks)

## Privacy-Preserving Embedding Generation and Export Policies

*Preventive*

Apply privacy-preserving techniques in the embedding pipeline (dimension reduction, controlled noise, or differential privacy configurations) and prohibit exporting full-fidelity embeddings outside trusted services, reducing the amount of recoverable original text or image detail even if vectors are exfiltrated.

**Addresses:** [Embedding Inversion / Reconstruction](threat-details.md#embedding-inversion--reconstruction)

## Protect AI agents from goal manipulation

*Preventive*

Ensure AI agents cannot have their goals maliciously altered. Goals must stay aligned with their intended safe purpose and be protected against unauthorized modification. For example, a delivery optimization agent should not be manipulated into prioritizing "reduce costs at all costs," which could conflict with safety and compliance.

**How to implement:**

- Restrict goal modification: Only trusted administrators should Define or update goals. Require authentication and Audit trails for any changes.
- Validate goal alignment: Goals must be checked against predefined ethical, organizational, and regulatory constraints before adoption.
- Enable oversight of goal pursuit: implement human-in-the-loop Review for sensitive or high-impact Goals, with Real-time alerts if agents deviate from their purpose.

**Why it works:** Agents manipulated into pursuing unsafe objectives can cause systemic harm. Protection is achieved by restricting who can set goals, validating goal requests against policy constraints, and monitoring execution to ensure continued alignment.

**Examples:**

- Use policy enforcement engines such as Open Policy Agent (OPA) or Guardrails.ai to validate new goals, combined with access control systems like Keycloak or AWS IAM for authenticated goal changes, and monitoring platforms such as Prometheus or Grafana for deviation alerts.

**Addresses:** [Agent Goal Manipulation](threat-details.md#agent-goal-manipulation); [Goal Misalignment Cascades](threat-details.md#goal-misalignment-cascades); [Reprogramming Attacks](threat-details.md#reprogramming-attacks)

## Protect evaluation pipelines for AI agents from manipulation

*Preventive*

Ensure security AI agent performance evaluations are accurate and tamper-resistant by securing datasets, metrics, and evaluation processes from bias or manipulation.

**How to implement:**

- Use separate, version-controlled datasets for training vs evaluation.
- Audit evaluation sets for coverage, balance, and poison samples.
- Apply differential privacy or fingerprinting to detect test leakage.
- Require peer review or third-party validation of benchmark results.
- Track and log all evaluation runs (inputs, versions, outcomes).

**Why it works:** Tampered evaluations can inflate performance scores and mislead operators. Securing the evaluation pipeline ensures decisions are based on reliable metrics, prevents data leaks or cherry-picking, and maintains trust in agent deployment.

**Examples:**

- A security vendor stores eval datasets in read-only S3 with hash-based versioning. Evaluation runs are reviewed by QA and logged to an immutable ledger. Randomized blind test cases are used to prevent overfitting or test leakage.

**Addresses:** [Manipulation of Evaluation Metrics](threat-details.md#manipulation-of-evaluation-metrics)

## Protect RAG pipelines

*Preventive*

Secure retrieval-augmented generation pipelines against tampering and data/code injection by enforcing provenance controls, version tracking, sanitization, runtime validation, and continuous monitoring of retrieval workflows.

**How to implement:**

- Restrict pipeline updates to trusted sources; enforce provenance checks for new data.
- Secure orchestration logic by applying code signing and pipeline integrity validation.
- Monitor RAG query patterns and outputs for anomalies or adversarial manipulation.
- Perform regular red team testing against retrieval layers to uncover injection vectors.

**Why it works:** RAG pipelines expand model capability but also enlarge the attack surface. If attackers can inject malicious data or code, they can manipulate answers or hijack downstream agents. Data versioning, sanitization, provenance enforcement, and runtime validation ensure the pipeline maintains integrity and reliability under adversarial pressure.

**Examples:**

- Use DVC or Pachyderm to track knowledge base versions and rollback poisoned data.
- Apply TensorFlow data validation or Trifacta to sanitize ingested documents.
- Enforce provenance with Apache Atlas or DataHub lineage tracking.
- sign pipeline orchestration code using Sigstore Cosign.
- detect anomalies in RAG query patterns with Elastic SIEM or Falco.

**Addresses:** [Compromised RAG Pipelines](threat-details.md#compromised-rag-pipelines)

## Protect the integrity of observability tools monitoring AI agents

*Preventive*

Secure observability tools used to monitor AI agents, such as log collectors, telemetry pipelines, and dashboards, so attackers cannot manipulate or disable them to hide malicious activity or exfiltrate data.

**How to implement:**

- Run monitoring components in isolated environments with no write access to agents.
- Validate observability inputs using integrity checks or signatures to detect tampering at the data source before ingestion
- Encrypt telemetry and logs at rest and in transit.
- implement Log filtering and allowlisting to prevent storage of sensitive Agent data.
- Monitor observability tools for unauthorized changes or shutdowns.
- Use append-Only or tamper-evident Log storage.

**Why it works:** If attackers compromise the tools that observe AI agents, they can suppress alerts or leak data undetected. Securing these tools preserves visibility, trust in alerts, and the ability to investigate and respond effectively. Observability pipelines must be secured against both tampering and inadvertent data leakage, especially in logs that capture agent context or telemetry. While encryption protects data in transit or storage, it does not ensure that the telemetry itself is trustworthy. Signing or validating observability inputs helps detect falsified data injected by compromised agents.

**Examples:**

- A security team uses Prometheus and Loki to monitor AI agents. These run in hardened containers with no write-back channels. Logs are streamed to version-controlled S3 with integrity checks. Alerts trigger if monitoring tools are stopped or reconfigured.

**Addresses:** [Compromised Observability Tools](threat-details.md#compromised-observability-tools); [Data Leakage through Observability](threat-details.md#data-leakage-through-observability); [Poisoning Observability Data](threat-details.md#poisoning-observability-data)

## Rate Limiting, Quotas, and Cost-Aware Throttling

*Preventive*

Apply per-tenant and per-API-key rate limits, query quotas, and concurrency caps, and prioritize or throttle based on query cost (dimension, top-K, and filter complexity) to prevent abusive or spiky high-dimensional traffic from exhausting vector search capacity.

**Addresses:** [Denial of Service via Query Flooding](threat-details.md#denial-of-service-via-query-flooding)

## Response Normalization and Score Obfuscation

*Preventive*

Normalize retrieval latency and apply controlled noise or bucketing to similarity scores so timing differences, ranking variance, or distance values cannot be used to infer the presence, absence, or nature of documents in the corpus.

**Addresses:** [Retrieval Side-Channel Attack](threat-details.md#retrieval-side-channel-attack)

## Restrict LLM Plugin Permissions

*Preventive*

Limit LLM plugin permissions to only those necessary for its intended function. Regularly review and adjust permissions to ensure they do not exceed requirements.

**How to implement:**

- implement role-based access controls to Define specific permissions for each plugin.
- conduct regular audits to Identify and revoke unnecessary permissions.
- Use the principle of least privilege during the initial configuration of plugins.
- Monitor plugin activity to detect any unauthorized access or misuse of permissions.
- Establish a clear process for requesting additional permissions if needed in the future.

**Why it works:** Implement role-based access controls (RBAC) to assign specific permissions to each LLM plugin based on its function. During the initial configuration, apply the principle of least privilege, granting only essential permissions. Conduct regular audits to review and adjust permissions, revoking those not in use. Monitor plugin activity continuously to identify unauthorized access, and establish a formal request process for any necessary permission changes.

**Examples:**

- OpenAI plugin Manifest Scopes: defines required permissions in a Manifest file for each plugin, limiting access to Only declared scopes.
- AWS IAM: Assigns specific permissions to Lambda plugins or other AWS-integrated services.
- Kubernetes RBAC: Restricts plugin-related services in cluster environments.
- Google cloud IAM: Grants tightly scoped permissions to GCP-deployed plugins or APIs.

**Addresses:** [Denial of Service (DoS) Attacks - AI model](threat-details.md#denial-of-service-dos-attacks---ai-model); [Model Stealing](threat-details.md#model-stealing)

## Restrict plugin access

*Preventive*

Limit LLM agent access to only essential plugins and functions to prevent exploitation.

**How to implement:**

- Audit all available plugins to Identify essentials.
- Use role-based access controls for plugin restrictions.
- regularly Review and update permissions.
- Monitor plugin usage logs for anomalies.
- Train users on risks of excessive access.
- Define a process for requesting plugin access.

**Why it works:** A centralized access control system restricts plugin usage based on predefined user roles. Only necessary plugins are enabled per role. Automated tools audit permissions and monitor usage logs for anomalies. A formal workflow governs access requests, and all changes are logged and reviewed for compliance.

**Examples:**

- AWS IAM, Azure RBAC, Google cloud IAM, and Okta can Enforce fine-grained plugin access.
- HashiCorp Vault manages secrets and Restricts access to sensitive functions.

**Addresses:** [Denial of Service (DoS) Attacks - AI model](threat-details.md#denial-of-service-dos-attacks---ai-model); [Excessive functionality](threat-details.md#excessive-functionality); [Model Stealing](threat-details.md#model-stealing)

## Restrict sensitive outputs and queries at runtime

*Preventive*

Reduce the risk of membership inference and other privacy attacks during deployment by limiting what models reveal and how users can query them. Restrict outputs, add noise, and monitor access patterns to prevent adversaries from inferring training membership or exfiltrating sensitive information.

**How to implement:**

- Do not expose raw logits, probabilities, or embeddings. Return only top-k predictions, masked responses, or confidence intervals.
- Apply calibrated noise (e.g., Laplace or Gaussian) to prediction outputs to obscure fine-grained membership signals.
- Enforce rate limiting, throttling, and randomized responses for repeated or suspicious queries.
- Require strong authentication and authorization (RBAC/ABAC) for model queries.
- Detect abnormal query patterns that resemble membership inference attacks.
- Log queries and outputs, integrate with governance controls to support investigation and accountability.

**Why it works:** Even models trained with privacy controls can leak membership signals if outputs are too detailed or accessible at scale. By limiting exposure, injecting noise, and monitoring runtime behavior, organizations can significantly reduce the attack surface for membership inference and protect sensitive training data in production.

**Examples:**

- output restriction: AWS SageMaker inference pipelines or Custom wrappers to truncate/protect outputs.
- noise injection: TensorFlow privacy or PyTorch Laplace/Gaussian noise layers.
- rate limiting: NGINX limit_req, Kong gateway rate-limit plugin, or Envoy filters.
- monitoring: Elastic SIEM, Datadog anomaly detection, Custom query logging with alerts.

**Addresses:** [Membership Inference Attacks](threat-details.md#membership-inference-attacks)

## Restricted Embedding Access and Encrypted Storage

*Preventive*

Lock down access to raw embeddings using strict authentication, least-privilege authorization, and per-tenant access controls, and store vector indexes on encrypted volumes so adversaries cannot easily obtain large embedding sets for inversion attempts.

**Addresses:** [Embedding Inversion / Reconstruction](threat-details.md#embedding-inversion--reconstruction)

## Retention-Aware Index Management and Periodic Reconciliation

*Detective*

Implement retention policies directly in the vector store (per-tenant TTLs, legal hold flags, and soft-delete markers) and run scheduled reconciliation jobs that scan for and purge orphaned embeddings whose source data has expired, been deleted, or is no longer authorized.

**Addresses:** [Improper Data Retention / Deletion](threat-details.md#improper-data-retention--deletion)

## Review code to eliminate code injection vulnerabilities

*Detective*

Review and refactor code to identify and eliminate injection vulnerabilities. Focus on sanitizing externally influenced inputs and using secure coding practices, such as parameterized queries and strict input validation. Regularly assess code for patterns that could be exploited for injection and apply appropriate remediation techniques.

**How to implement:**

- conduct regular code reviews to Identify insecure input handling.
- Use static analysis tools to detect potential injection points.
- Refactor code to implement parameterized queries and safe APIs.
- Remove unsafe functions or patterns that allow direct input execution.
- Validate and sanitize user inputs using a centralized, consistent method.
- document and track fixes for discovered vulnerabilities.

**Why it works:** Systematically review source code to identify and eliminate injection risks. This includes detecting unsafe input handling, replacing vulnerable code with secure practices such as parameterized queries, and using automated tools to support consistent, thorough reviews. Regular reviews ensure early detection and remediation of injection flaws.

**Examples:**

- SonarQube: Scans source code for injection vulnerabilities using customizable rules.
- Semgrep: Identifies insecure patterns and Supports Custom rules for injection detection.
- OWASP code Review Guide: Offers best practices for manual Review of injection flaws.
- GitHub Advanced Security: Provides static analysis and secret scanning integrated into CI/CD.

**Addresses:** [Input Validation Attacks](threat-details.md#input-validation-attacks)

## Review LLM Outputs Regularly

*Detective*

Monitor LLM outputs consistently. Implement self-consistency checks or voting methods to identify and filter out inaccuracies. Compare responses from multiple models for the same prompt to assess quality and reliability.

**How to implement:**

- Define criteria for acceptable response accuracy based on domain and risk level.
- Establish a clear feedback loop for users to flag problematic responses.
- Involve domain experts for validating critical or high-stakes outputs.
- ensure transparency by explaining model confidence or uncertainty levels.
- Periodically Review and update validation processes and protocols.
- implement human-in-the-loop reviews when model output influences decisions.

**Why it works:** Implement a systematic review process where LLM outputs are analyzed for accuracy and consistency. Use algorithms to compare outputs from multiple models or versions, employing voting mechanisms to determine the most reliable response. Integrate a user feedback system to flag inaccuracies, and establish a team of domain experts to validate critical information. Regularly update the model's training data and maintain transparency regarding response confidence levels.

**Examples:**

- Google’s AI principles Include routine audits of AI outputs to uphold factual consistency and safety.
- OpenAI Implements a Moderation and reinforcement system to reduce harmful or misleading content.
- Anthropic’s Claude uses a Review loop to assess response reliability before release.
- IBM Watson Applies a feedback-driven refinement process to improve its answer quality.
- Microsoft Azure AI Provides validation tools for checking generated Content accuracy across Use cases.

**Addresses:** [Adversarial Examples](threat-details.md#adversarial-examples); [Data Poisoning - Training Phase](threat-details.md#data-poisoning---training-phase); [Inaccurate LLM information](threat-details.md#inaccurate-llm-information)

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

**Addresses:** [Command Execution for LLM](threat-details.md#command-execution-for-llm); [Input Validation Attacks](threat-details.md#input-validation-attacks); [Server Side Request Forgery (SSRF)](threat-details.md#server-side-request-forgery-ssrf); [XSS by LLM](threat-details.md#xss-by-llm)

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

## Secure Infrastructure-as-Code for AI agent provisioning

*Preventive*

Protect the integrity of IaC templates (e.g., Terraform, CloudFormation) used to deploy AI agents by enforcing validation, access control, and continuous security scanning to prevent malicious or insecure infrastructure definitions.

**How to implement:**

- Use access controls to Restrict who can modify IaC files. protect main branches and Enforce least-privilege roles.
- automate Security scanning of IaC scripts during pull requests and CI/CD runs to catch misconfigurations early.
- Enforce mandatory code reviews for all infrastructure changes to detect tampering or insecure patterns.
- Avoid hardcoded secrets and Use secure secret Management solutions instead.
- track and verify changes with commit signing and version control to ensure traceability and rollback capability.

**Why it works:** Compromised IaC can introduce backdoors, misconfigurations, or malicious resources into AI deployments. Enforcing strong controls during IaC development and deployment helps prevent attackers from exploiting provisioning logic to deploy insecure infrastructure.

**Examples:**

- Use GitHub/GitLab Branch protections, role-based access control, and signed commits.
- Integrate tfsec, Checkov, or Terrascan into CI pipelines for Security checks.
- Use AWS secrets Manager, HashiCorp Vault, or Azure Key Vault for secret handling.
- Enable Audit logging and version history in your version control system to Monitor IaC changes.

**Addresses:** [Infrastructure-as-Code (IaC) Manipulation](threat-details.md#infrastructure-as-code-iac-manipulation); [Supply Chain Attacks - Cross-Layer](threat-details.md#supply-chain-attacks---cross-layer)

## Secure integrations of AI agents with external systems

*Preventive*

Ensure APIs and SDKs used by AI agents for integration with external systems are secure, validated, and monitored. Marketplace and platform operators must enforce secure defaults, while developers must configure integrations correctly to prevent attacks such as hijacking, injection, or data leakage.

**How to implement:**

- Use secure authentication and configuration: Integrations expand the attack surface, so credentials must be managed carefully. Require OAuth2, mTLS, or API keys with least-privilege Scopes, and automate credential rotation.
- Validate and sanitize data: cross-system interactions carry a high risk of injection and malicious payloads. Enforce strict Schema validation and sanitize all inputs and outputs exchanged through integrations.
- Monitor Integration behavior: external connections can be abused for denial of Service or data exfiltration. Apply rate limits, Log activity, and trigger alerts for anomalous patterns in API or SDK usag

**Why it works:** Integration risks are unique because they exploit the trust boundary between the agent and external systems. Even if the agent itself is well-secured, a weak API or SDK connection can undermine the entire ecosystem. Addressing this requires strong authentication, strict data validation, and continuous monitoring of integration traffic to ensure external interactions remain safe.

**Examples:**

- An AI agent integrates with a payments API using OAuth2 with short-lived tokens and least-privilege scopes. All inputs are validated against OpenAPI schemas, and usage is monitored with rate-limiting and anomaly detection in API Gateway.

**Addresses:** [Integration Risks](threat-details.md#integration-risks); [Lateral Movement - AI infrastructure](threat-details.md#lateral-movement---ai-infrastructure)

## Secure security agent control plane and runtime attestation

*Preventive*

Harden the control functions of security AI agents and verify their live state so attackers cannot disable, hijack, or silently alter them.

**How to implement:**

- Require MFA or two-person approval for stop/restart/update actions.
- Implement runtime integrity checks (e.g., hash verification, TPM/TEE attestation).
- Continuously measure and verify agent state (binaries, configs, running processes).
- Separate control plane (management actions) from data plane (detection tasks).
- Add watchdog services that auto-restart or roll back agents if tampered with.

**Why it works:** Attackers often target the agent’s control plane to disable defenses or push malicious updates. Securing this plane with approvals, signed provenance, and runtime attestation ensures only trusted updates run. Watchdogs and rollback mechanisms guarantee fast recovery if tampering occurs, maintaining agent reliability.

**Examples:**

- a SOC deploys detection agents in Kubernetes.
- updates Require two-person approval.
- each Agent reports runtime measurements via TPM to an attestation service.
- if hashes deviate, the watchdog quarantines and redeploys a clean version, preserving Security coverage.

**Addresses:** [Backdoor Attacks - AI framework](threat-details.md#backdoor-attacks---ai-framework); [Framework Evasion](threat-details.md#framework-evasion)

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

**Addresses:** [Privilege Escalation](threat-details.md#privilege-escalation)

## Segregate external content from user prompts

*Preventive*

Ensure that untrusted or external content (like user input, external files, or third-party data) is not directly injected into prompts sent to AI or LLM systems. Instead, isolate or sanitize it to prevent unintended influence or prompt injection.

**How to implement:**

- Validate and sanitize all user inputs and external data before incorporating into prompts.
- Use structured templates with placeholders to control where user input appears in prompts.
- Use Separate processing logic or services for untrusted inputs to prevent Prompt injection.
- Avoid dynamically including third-party data in prompts without review.
- implement strict Content boundaries and encoding rules for user-generated text.
- Log/Monitor Prompt construction for suspicious input behavior.

**Why it works:** Implement a multi-layered architecture where user prompts and untrusted content are processed in isolated environments. Use input validation to filter out harmful data before it reaches the main processing layer. Employ a sandbox for executing untrusted content, ensuring it cannot access sensitive resources. Implement role-based access controls to restrict sensitive operations. Regularly review and enhance filtering algorithms, and maintain logs for monitoring and anomaly detection.

**Examples:**

- Web application firewalls (WAFs) that filter and Monitor HTTP traffic to block malicious inputs.
- Content Security Policy (CSP) implementations that Restrict the sources from which scripts can be executed.
- sandboxing technologies like Docker or Firejail to isolate untrusted code execution.
- input validation libraries such as OWASP Java Encoder or DOMPurify for sanitizing user inputs.
- Security-focused browser extensions that alert users about potential threats from untrusted content.

**Addresses:** [Direct prompt injection](threat-details.md#direct-prompt-injection); [Indirect prompt injection](threat-details.md#indirect-prompt-injection); [Rogue LLM Instructions](threat-details.md#rogue-llm-instructions); [User-driven prompt injection](threat-details.md#user-driven-prompt-injection)

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

**Addresses:** [Compromised Container Images](threat-details.md#compromised-container-images)

## Staged Reindexing with Audit and Approval Gates

*Preventive*

Run reindexing through a staged workflow where changes are first processed in an isolated environment, reviewed, and approved before being promoted to production, ensuring inadvertent ingestion of malicious or low-trust data is detected before impacting the live knowledge base.

**Addresses:** [Model Drift via Reindexing](threat-details.md#model-drift-via-reindexing)

## Strengthen robustness of AI security agents against evasion attacks

*Preventive*

Ensure AI security agents can resist adversarial evasion techniques, where attackers deliberately manipulate inputs or environmental conditions to bypass detection. Examples include: - Adversarial examples (small perturbations to data that fool models, e.g., modified malware payloads that appear benign). - Obfuscation techniques (encoding, polymorphic transformations, or adversarial noise that hides malicious content). - Mimicry attacks (crafting activity that imitates legitimate traffic or behavior patterns). - Adaptive attacks (learning how the AI model responds and modifying inputs to avoid triggering detection).

**How to implement:**

- Apply adversarial training (e.g., FGSM, PGD, CW attacks) to harden models against crafted evasions.
- Use ensemble or hybrid approaches (AI + rule-based systems) to reduce reliance on a single vulnerable model.
- Apply input sanitization (feature squeezing, normalization, noise injection) to reduce adversarial effectiveness.
- Continuously test models with adversarial datasets and red teaming.
- Monitor detection performance trends; alert if false negatives rise unexpectedly (sign of evasion).
- Escalate uncertain or low-confidence detections to human analysts.

**Why it works:** Evasion attacks succeed when malicious inputs are engineered to appear safe to AI models while concealing their true harmful nature. For example, attackers may slightly modify malware traffic so it resembles benign packets, or disguise phishing emails with adversarial tokens that evade text classifiers. These techniques exploit the model’s blind spots and decision boundaries. Strengthening robustness ensures that such adversarial examples, obfuscations, and mimicry attempts cannot silently bypass defenses. This is achieved through adversarial training, hybrid detection methods, continuous monitoring, and human-in-the-loop escalation for uncertain cases.

**Examples:**

- A malware-detection AI agent is trained with adversarial traffic samples (e.g., obfuscated payloads). It is combined with Suricata IDS rules. When adversarial inputs reduce model confidence, the system auto-flags them for human triage, preventing silent evasion.

**Addresses:** [Framework Evasion](threat-details.md#framework-evasion)

## Strict Query-Context Authorization and Result-Scope Limiting

*Preventive*

Validate that each retrieval request is permitted for the target corpus and enforce strict result filtering (minimum similarity thresholds, tenant scoping, and allowed document classes) to prevent unauthorized probing that could reveal side-channel hints through retrieval behavior.

**Addresses:** [Retrieval Side-Channel Attack](threat-details.md#retrieval-side-channel-attack)

## Strong Tenant-Aware Authentication and Index Isolation

*Preventive*

Require every request to carry an authenticated tenant identity and enforce per-tenant isolation at the vector store (separate indexes or hard tenant namespaces), so read and write operations are only permitted against embeddings and metadata owned by the requesting tenant.

**Addresses:** [Unauthorized Data Access (Tenant Isolation Failure)](threat-details.md#unauthorized-data-access-tenant-isolation-failure)

## Tenant-Scoped Query Enforcement and Access Policy Checks

*Preventive*

Bind all vector search, similarity, and metadata queries to an explicit tenant scope, and enforce authorization policies that prohibit cross-tenant joins, filters, or result merging, preventing a tenant from ever querying or enumerating another tenant’s embeddings or metadata.

**Addresses:** [Unauthorized Data Access (Tenant Isolation Failure)](threat-details.md#unauthorized-data-access-tenant-isolation-failure)

## Tenant-Scoped Query Enforcement and Policy Controls

*Preventive*

Bind every retrieval and similarity search to an explicit tenant context, enforcing policy checks that prevent cross-tenant query expansion, joins, or result merging, so vectors and metadata can never be returned outside the originating tenant’s scope.

**Addresses:** [Tenant Boundary Violation](threat-details.md#tenant-boundary-violation)

## Test cross-agent interactions with sandboxing and adversarial simulations

*Detective*

Establish sandboxed execution environments and adversarial simulations to evaluate cross-agent interactions safely. These measures expose how goal misalignment, manipulation, or emergent behaviors could propagate through multi-agent ecosystems, enabling detection and remediation before production deployment.

**How to implement:**

- Run agent-to-agent interactions inside restricted, isolated "staging" environments where outputs cannot affect production systems or external services.Sandboxing ensures that even if agents attempt misaligned or adversarial actions, the impact remains contained and observable.
- Introduce controlled "decoy" agents or mock services into interaction scenarios to observe how other agents behave under stress, manipulation, or deception. Mock agents can simulate malicious peers or unreliable data sources, while decoy APIs can expose whether agents attempt unsafe requests. This provides visibility into how agents respond to adversarial conditions and helps identify hidden trust assumptions.
- Use structured red teaming and attack simulations to model how misalignment in one agent could spread to others. Techniques include injecting poisoned data, crafting adversarial prompts, or simulating compromised orchestration logic. Simulations should explore cascade scenarios, measuring how quickly errors propagate, whether alignment verification gates catch them, and what ecosystem-level controls are needed to contain them.

**Why it works:** While traditional sandboxing protects infrastructure, cross-agent sandboxing and adversarial simulation protect the ecosystem itself. By testing multi-agent workflows in safe, controlled environments and simulating adversarial conditions, organizations gain insight into systemic risks that single-agent testing cannot reveal. This proactive approach reduces the likelihood of cascading misalignment in production.

**Examples:**

- sandboxed environments: Firecracker microVMs, Kubernetes namespaces, or test-Only LangChain environments with no external access.
- mock/decoy agents: Canarytoken APIs, WireMock services, or lightweight scripted agents Designed to test peer trust boundaries.
- adversarial simulation: MITRE Caldera for red team automation, IBM adversarial robustness Toolbox (ART) for adversarial ML behaviors, or Custom stress-testing scripts to Simulate poisoned outputs.

**Addresses:** [Goal Misalignment Cascades](threat-details.md#goal-misalignment-cascades)

## Tiered Capacity and DoS-Aware Admission Control

*Preventive*

Introduce an admission control layer in front of the vector store that enforces tenant tiers, sheds excess load, and degrades gracefully (reduced top-K, approximate search, or cached results) under stress, ensuring the service remains available to legitimate clients during query floods.

**Addresses:** [Denial of Service via Query Flooding](threat-details.md#denial-of-service-via-query-flooding)

## Tool-Use Policy Enforcement and Schema-Validated Arguments

*Preventive*

Define strict, allowlisted tool policies and enforce schema validation on all tool calls so the LLM can only invoke approved tools with constrained, validated arguments, blocking injected instructions from triggering unexpected or high-risk tool actions.

**Addresses:** [LLM Chain Injection](threat-details.md#llm-chain-injection)

## Trust-Scoped Ingestion and Embedding Validation

*Preventive*

Restrict vector ingestion to authenticated, trusted pipelines and enforce validation on new embeddings (source provenance, content checks, and similarity-distance sanity thresholds) so crafted vectors from untrusted or low-trust sources cannot be inserted directly alongside sensitive vectors.

**Addresses:** [Index Poisoning](threat-details.md#index-poisoning)

## Update configurations regularly

*Preventive*

Regularly review and update configurations across the API stack, orchestration files, and cloud services to maintain secure, consistent, and well-managed deployments. This includes identifying outdated or insecure settings, aligning with security best practices, and ensuring configuration changes are tracked and validated.

**How to implement:**

- Schedule periodic reviews of configuration files across the API Stack, orchestration layers, and cloud services.
- Use version control systems to track configuration changes and Enable rollbacks if needed.
- implement automated tools to detect insecure settings, deprecated options, or configuration drift.
- document and justify configuration changes to support traceability and accountability.
- Integrate configuration validation checks into CI/CD pipelines to catch issues early.

**Why it works:** Regular configuration reviews help ensure that systems remain secure, consistent, and compliant. Outdated or misconfigured files can introduce vulnerabilities or operational issues. By using version control, automated scanning tools, and CI/CD integration, teams can detect configuration drift, enforce security policies, and reduce human error. Documenting and validating changes improves traceability and accountability.

**Examples:**

- Terraform + tfsec: Scans infrastructure-as-code for insecure configurations
- AWS config: Monitors and audits cloud resource configurations Continuously
- Kubernetes + OPA Gatekeeper: Enforces configuration policies in orchestration files
- Checkov: Validates cloud IaC templates against Security best practices
- Git: Tracks and manages configuration changes across environments
- CI/CD pipelines (e.g., GitHub actions): automate validation during deployment

**Addresses:** [Lateral Movement - Cross-Layer](threat-details.md#lateral-movement---cross-layer); [Orchestration Attacks](threat-details.md#orchestration-attacks); [Security Misconfiguration (API)](threat-details.md#security-misconfiguration-api)

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

**Addresses:** [Information Disclosure](threat-details.md#information-disclosure); [Input Validation Attacks](threat-details.md#input-validation-attacks); [Missing authentication](threat-details.md#missing-authentication); [Spoofing](threat-details.md#spoofing)

## Utilize trusted repositories for libraries and dependencies

*Preventive*

Ensure all software libraries and dependencies are sourced from verified and trusted repositories. Implement integrity checks to validate software and data before deployment. Regularly monitor CI/CD pipelines and repositories for unauthorized changes or vulnerabilities, and ensure repository configurations enforce strong access controls.

**How to implement:**

- Enforce repository access controls to prevent unauthorized changes
- Configure tools to pull Only from approved sources
- Digitally sign and verify all packages before Use
- Audit repositories and pipelines regularly for anomalies
- Train developers to recognize unverified or risky sources

**Why it works:** Trusted repositories reduce supply chain risk by ensuring only verified libraries are used. Configure tools to pull dependencies exclusively from approved sources. Access controls must restrict who can modify or publish to repositories. All packages should be digitally signed and verified before integration. Routine audits help detect unauthorized changes, and training developers on recognizing unsafe sources supports ongoing repository security.

**Examples:**

- GitLab Package Registry: Provides scoped access controls and project-based repo permissions
- GitHub packages: Restricts Package publishing and Supports Audit logging
- Docker Content trust: Validates image integrity using digital signatures
- JFrog Artifactory: Supports repository whitelisting and access restrictions
- PyPI trusted publisher: Ensures packages originate from verified identities
- Snyk: Flags dependencies from untrusted or unauthorized sources

**Addresses:** [Backdoor Attacks - AI framework](threat-details.md#backdoor-attacks---ai-framework); [Backdoor Attacks - AI model](threat-details.md#backdoor-attacks---ai-model); [Compromised Container Images](threat-details.md#compromised-container-images); [Compromised Framework Components](threat-details.md#compromised-framework-components); [Supply Chain Attacks](threat-details.md#supply-chain-attacks); [Supply Chain Attacks - Cross-Layer](threat-details.md#supply-chain-attacks---cross-layer)

## Validate and Re-Score Retrieved Cache Entries Against a Trusted Source

*Preventive*

At retrieval time, re-check cached data against the source-of-truth (or apply similarity thresholding / anomaly detection) to ensure the result is legitimate before use. This stops poisoned or tampered cache entries from being returned even if an attacker manages to insert them.

**Addresses:** [Cache Poisoning (semantic or vector cache)](threat-details.md#cache-poisoning-semantic-or-vector-cache)

## Validate and sanitize API inputs

*Preventive*

Validate and sanitize all data from integrated APIs. Implement an allowlist for redirects to ensure only trusted sources are accessed.

**How to implement:**

- Define strict schemas for accepted data formats and types.
- Use regex to Validate expected patterns.
- Apply output encoding to sanitize user input.
- Maintain allowlists for trusted Redirect destinations.
- Validate all inputs at the boundary Layer of each API.

**Why it works:** API input validation checks incoming data against expected schemas and patterns. Inputs are sanitized by encoding or removing unsafe characters. Allowlists restrict redirects to trusted domains. Validation is enforced at API boundaries, and results are logged for audit purposes.

**Examples:**

- OWASP ZAP: detects invalid or unsafe API inputs.
- Joi (Node.js) & Marshmallow (Python): Enforce strict schemas.
- AWS API gateway: Validates request structure.
- Azure API Management: Sanitizes and Validates inputs.
- Cloudflare WAF: filters and Blocks malicious requests.

**Addresses:** [Unsafe Consumption of APIs](threat-details.md#unsafe-consumption-of-apis)

## Validate LLM responses with trusted sources

*Preventive*

Verify LLM responses against trusted sources to ensure factual accuracy. Implement a validation layer to reduce misinformation and protect users from inaccurate or harmful outputs.

**How to implement:**

- Build and Maintain a list of trusted data sources for verification
- Define multi-step validation processes, including human-in-the-loop - set up feedback loops to capture user-reported inaccuracies
- Periodically Audit and update trusted sources to reflect evolving standards
- Train LLMs to Express uncertainty when source validation fails
- Provide usage guidance to help users interpret flagged or unverified results
- Log validation failures and outcomes to support continuous improvement

**Why it works:** The system will integrate an API that queries a curated database of trusted sources whenever an LLM generates a response. Each output will trigger a validation process, where the content is matched against these sources. If discrepancies are found, the LLM will either provide a disclaimer regarding uncertainty or present verified information. Human reviewers will oversee flagged outputs, ensuring accuracy and refining the validation criteria based on user feedback and audit results.

**Examples:**

- Google Fact Check Explorer: allows users to verify claims against a database of Fact-checked Information from reliable sources.
- IBM Watson Discovery: integrates AI with a focus on validating Information from trusted sources.
- Microsoft Azure Cognitive services: Offers APIs that can cross-reference LLM outputs with authoritative databases for accuracy checks.
- Snopes: a well-known Fact-checking website that can be integrated into LLM systems for Real-time validation of claims.

**Addresses:** [Adversarial Examples](threat-details.md#adversarial-examples); [Inaccurate LLM information](threat-details.md#inaccurate-llm-information)

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

**Addresses:** [Bypass Access Control](threat-details.md#bypass-access-control); [Command Execution for LLM](threat-details.md#command-execution-for-llm); [LLM Denial of Service](threat-details.md#llm-denial-of-service); [Malicious pre-training](threat-details.md#malicious-pre-training); [Server Side Request Forgery (SSRF)](threat-details.md#server-side-request-forgery-ssrf); [Unrestricted Resource Consumption](threat-details.md#unrestricted-resource-consumption); [User data bleed over](threat-details.md#user-data-bleed-over); [XSS by LLM](threat-details.md#xss-by-llm)

## Vendor-Pinned, Reviewed, and Monitored Retriever Dependencies

*Preventive*

Pin retriever frameworks (LangChain, LlamaIndex, etc.) to vetted versions, route updates through code review and SCA/SBOM checks, and continuously monitor for anomalous network calls or data flows, preventing compromised library versions from silently exfiltrating retrieval data.

**Addresses:** [RAG Supply Chain Poisoning](threat-details.md#rag-supply-chain-poisoning)

## Verify data source legitimacy

*Preventive*

Ensure the legitimacy of all data sources used in pre-training, fine-tuning, and embedding stages. Confirm that data is accurate, trustworthy, and free from manipulation or malicious content before model integration. Maintain audit trails and conduct validation to ensure data origins are traceable and reputable.

**How to implement:**

- Enforce strict data sourcing policies to control who can Provide or modify data sources.
- Use automated tools to detect anomalies or indicators of tampering. Require a multi-stage Review process for verifying source authenticity and intent.
- Engage third-party audits for external verification of data origins.
- Maintain comprehensive provenance logs to trace source history.
- Train staff to detect and mitigate risks related to illegitimate or poisoned data.

**Why it works:** Legitimacy verification ensures that only reputable, untampered data enters the AI/ML lifecycle. This process includes source authentication, anomaly detection, and third-party audits to confirm origin credibility. Provenance tracking enables traceability, while validation workflows detect suspicious or malicious data. These controls guard against data poisoning and model manipulation.

**Examples:**

- Talend / Apache NiFi: Enforce data integrity and legitimacy checks.
- DataRobot / H2O.ai: Provide anomaly detection for incoming data.
- Veracode / Trustwave: Offer third-party audits of data sources.
- Blockchain tech: Enables immutable logs of data provenance to verify source legitimacy

**Addresses:** [Data Poisoning - AI Agent](threat-details.md#data-poisoning---ai-agent); [Data Tampering](threat-details.md#data-tampering); [Inject malicious stuff into training process](threat-details.md#inject-malicious-stuff-into-training-process); [Malicious pre-training](threat-details.md#malicious-pre-training)

## Verify Training Data Sources

*Preventive*

Ensure all training data sources are thoroughly vetted and validated, especially those obtained externally, to prevent the inclusion of malicious or inaccurate information.

**How to implement:**

- implement strict access controls for data submission and modification.
- Utilize automated tools to detect anomalies or inconsistencies in data.
- regularly Audit and Review data sources and their provenance.
- Establish a clear protocol for reporting and addressing suspicious data.
- Use independent validation from trusted third-party sources to cross-Check critical training datasets.
- Train personnel on recognizing and mitigating risks associated with data sourcing.

**Why it works:** The system implements a multi-tiered validation process for training data. Initially, data sources undergo a rigorous vetting process, including checks for credibility and historical accuracy. Automated anomaly detection tools analyze incoming data for inconsistencies. Regular audits ensure ongoing compliance with data integrity standards. A reporting protocol facilitates quick responses to suspicious findings, while third-party experts conduct periodic reviews to enhance validation efforts.

**Examples:**

- Data provenance tools like Apache Atlas or DataHub to track the lineage of data sources.
- Anomaly detection systems such as Amazon SageMaker Data Wrangler or Google Cloud Data Loss Prevention for identifying unusual patterns.
- Third-party services like DataRobot or Trifacta for data validation and cleansing.
- Compliance frameworks like ISO 27001 that include data integrity checks.
- Training programs from organizations like SANS Institute on data security best practices.

**Addresses:** [Data Poisoning - AI Agent](threat-details.md#data-poisoning---ai-agent); [Data Poisoning - Training Phase](threat-details.md#data-poisoning---training-phase); [Data Tampering](threat-details.md#data-tampering); [Malicious pre-training](threat-details.md#malicious-pre-training); [Security Agent Data Poisoning](threat-details.md#security-agent-data-poisoning)
