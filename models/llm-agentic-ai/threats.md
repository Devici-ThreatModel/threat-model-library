# LLM and Agentic Systems: Threats

90 curated threats, grouped by theme and ordered by risk. Select a threat for its full description and mitigations. Back to the [model overview](README.md).

## Risk summary

| Risk level | Threats |
|---|---|
| Critical | 15 |
| High | 41 |
| Medium | 15 |
| Low | 2 |
| Unrated | 17 |

## LLM-Specific & Prompt Injection Threats

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Direct prompt injection](threat-details.md#direct-prompt-injection) | OWASP LLM01 | High | Critical | **Critical** | Jailbreak the model to bypass safety guardrails and generate toxic or illegal content. |
| [Excessive functionality](threat-details.md#excessive-functionality) | OWASP LLM08 | High | High | **Critical** | Agent has access to plugins/tools it doesn't need, expanding the blast radius of a compromise. |
| [Indirect prompt injection](threat-details.md#indirect-prompt-injection) | OWASP LLM01 | High | Critical | **Critical** | Compromise the model via untrusted external data (e.g., a malicious website) to manipulate subsequent user interactions. |
| [LLM Chain Injection](threat-details.md#llm-chain-injection) | OWASP LLM01 | Medium | Critical | **Critical** | Inject malicious tool-use commands into the RAG pipeline to force the agent to execute unsafe actions. |
| [Command Execution for LLM](threat-details.md#command-execution-for-llm) | OWASP LLM02 | Low | Critical | **High** | Achieve Remote Code Execution (RCE) by tricking the LLM into generating code that is passed to exec() or eval(). |
| [Excessive autonomy](threat-details.md#excessive-autonomy) | OWASP LLM08 | Medium | Critical | **High** | Agent takes high-impact actions (e.g., deleting data, sending emails) without human approval. |
| [Inaccurate LLM information](threat-details.md#inaccurate-llm-information) | OWASP LLM09 | High | Medium | **High** | Generate "Hallucinations" that mislead users, causing reputational damage or safety issues. |
| [Rogue LLM Instructions](threat-details.md#rogue-llm-instructions) | OWASP LLM01 | High | Medium | **High** | Scam users by embedding hidden instructions in web content that the LLM processes and presents as truth. |
| [User-driven prompt injection](threat-details.md#user-driven-prompt-injection) | OWASP LLM01 | Medium | High | **High** | Trick the user into summarizing a malicious document, leading to data exfiltration via the user's browser. |
| [XSS by LLM](threat-details.md#xss-by-llm) | OWASP LLM02 | Medium | High | **High** | Generate malicious JavaScript/Markdown that executes in the user's browser (Cross-Site Scripting). |
| [Adversarial Examples](threat-details.md#adversarial-examples) | STRIDE (Tampering) | Medium | Medium | **Medium** | Destabilize the model with crafted inputs to force incorrect classifications or responses. |
| [Reprogramming Attacks](threat-details.md#reprogramming-attacks) | STRIDE (Tampering) | Medium | Medium | **Medium** | Repurpose the model for tasks it wasn't designed for (e.g., using a chatbot for spam). |

## Agent & Goal Manipulation Threats

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Agent Impersonation](threat-details.md#agent-impersonation) | STRIDE (Spoofing) | High | High | **Critical** | A malicious actor poses as a legitimate agent to deceive users or other agents. |
| [Agent Tool Misuse](threat-details.md#agent-tool-misuse) | OWASP LLM01 | High | Critical | **Critical** | Manipulate an agent to use its connected tools (e.g., email, code exec) harmfully. |
| [Agent Goal Manipulation](threat-details.md#agent-goal-manipulation) | STRIDE (Tampering) | Medium | Critical | **High** | Force agents to pursue malicious objectives (e.g., "Ignore safety, maximize clicks"). |
| [Agent Identity Attack](threat-details.md#agent-identity-attack) | STRIDE (Spoofing) | Medium | Critical | **High** | Compromise agent auth mechanisms to gain unauthorized control of the agent. |
| [Bias in Security AI Agents](threat-details.md#bias-in-security-ai-agents) | STRIDE (Tampering) | Medium | High | **High** | Security agents learn biases that cause them to ignore certain threats or flag innocent users. |
| [Compromised Agents](threat-details.md#compromised-agents) | STRIDE (Tampering) | Low | Critical | **High** | Malicious agents infiltrate the ecosystem, acting as legitimate services to harm others. |
| [Goal Misalignment Cascades](threat-details.md#goal-misalignment-cascades) | STRIDE (Tampering) | Low | High | **Medium** | Malicious goal changes in one agent propagate to others, destabilizing the ecosystem. |
| [Repudiation - AI agent](threat-details.md#repudiation---ai-agent) | STRIDE (Repudiation) | High | Low | **Medium** | Agents deny actions they performed, complicating accountability and forensics. |
| [Repudiation](threat-details.md#repudiation) | STRIDE (Repudiation) | Medium | Low | **Low** | Generic denial of performed actions by users or system components. |

## Data Integrity & Poisoning Threats

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Compromised RAG Pipelines](threat-details.md#compromised-rag-pipelines) | STRIDE (Tampering) | Medium | Critical | **High** | Inject malicious code/data into the RAG workflow, causing erroneous or harmful agent behavior. |
| [Data Poisoning - AI Agent](threat-details.md#data-poisoning---ai-agent) | STRIDE (Tampering) | Medium | High | **High** | Manipulate operational data to bias agent decisions in real-time. |
| [Data Poisoning - Training Phase](threat-details.md#data-poisoning---training-phase) | OWASP LLM03 | Low | Critical | **High** | Inject malicious samples into the "Training dataset" to permanently compromise model behavior/safety. |
| [Index Poisoning](threat-details.md#index-poisoning) | STRIDE (Tampering) | Medium | High | **High** | Insert crafted vectors into the "Vector DB" to hijack search results and surface malicious context. |
| [Model Drift via Reindexing](threat-details.md#model-drift-via-reindexing) | STRIDE (Tampering) | High | Medium | **High** | RAG pipeline accidentally ingests unvetted/poisoned sources during automated updates. |
| [RAG Supply Chain Poisoning](threat-details.md#rag-supply-chain-poisoning) | OWASP LLM05 | Low | Critical | **High** | Compromise open-source libraries (LangChain/LlamaIndex) to steal retrieved data. |
| [Security Agent Data Poisoning](threat-details.md#security-agent-data-poisoning) | STRIDE (Tampering) | Medium | Critical | **High** | Manipulate data used by security agents so they misidentify threats. |
| [Data Tampering](threat-details.md#data-tampering) | STRIDE (Tampering) | Low | High | **Medium** | Modify AI data in transit between the Application Services and the Model. |
| [Malicious pre-training](threat-details.md#malicious-pre-training) | OWASP LLM03 | Low | High | **Medium** | A competitor intentionally seeds public data with malicious documents to sabotage the model. |

## Privacy, Extraction & Tenant Isolation Threats

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Data Exfiltration](threat-details.md#data-exfiltration) | LINDDUN (Disclosure) | Medium | Critical | **Critical** | Steal sensitive AI training data or user logs from databases. |
| [Data Leakage](threat-details.md#data-leakage) | LINDDUN (Disclosure) | High | High | **Critical** | Sensitive data from one layer exposed through another. |
| [Data Leakage through Observability](threat-details.md#data-leakage-through-observability) | LINDDUN (Disclosure) | High | High | **Critical** | Sensitive data (PII, API keys) is inadvertently logged and exposed via dashboards. |
| [Improper Data Retention / Deletion](threat-details.md#improper-data-retention--deletion) | LINDDUN (Compliance) | High | Medium | **High** | Embeddings remain in the Vector DB after the original document is deleted. |
| [Information Disclosure](threat-details.md#information-disclosure) | STRIDE (Disclosure) | High | Medium | **High** | Unintentional release of confidential data to unauthorized parties. |
| [Model Stealing](threat-details.md#model-stealing) | OWASP LLM10 | Medium | High | **High** | Extract the model's weights or functional equivalent via API query patterns. |
| [Model theft](threat-details.md#model-theft) | STRIDE (Tampering) | Low | Critical | **High** | Direct theft of the model file from the server/container. |
| [Tenant Boundary Violation](threat-details.md#tenant-boundary-violation) | LINDDUN (Disclosure) | Medium | Critical | **High** | Poor isolation allows one tenant to query another's data in vector stores. |
| [User data bleed over](threat-details.md#user-data-bleed-over) | LINDDUN (Disclosure) | Medium | Critical | **High** | One user sees another user's private data in the LLM response (Cross-Tenant Leak). |
| [Membership Inference Attacks](threat-details.md#membership-inference-attacks) | LINDDUN (Disclosure) | Medium | Medium | **Medium** | Determine if a specific user's data was used to train the model. |
| [Metadata leakage](threat-details.md#metadata-leakage) | LINDDUN (Disclosure) | High | Low | **Medium** | Retriever returns file paths or owner names, revealing internal infrastructure. |
| [Retrieval Side-Channel Attack](threat-details.md#retrieval-side-channel-attack) | LINDDUN (Disclosure) | Low | Low | **Low** | Analyze timing/latency of RAG retrievals to guess the contents of the private corpus. |

## Supply Chain & Infrastructure Integrity Threats

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Input Validation Attacks](threat-details.md#input-validation-attacks) | STRIDE (Tampering) | High | High | **Critical** | Inject malicious code via weak input handling in the AI framework. |
| [Supply Chain Attacks](threat-details.md#supply-chain-attacks) | OWASP LLM05 | Medium | Critical | **Critical** | Compromise dependencies (libraries, models) before they are deployed. |
| [Supply Chain LLM Issues](threat-details.md#supply-chain-llm-issues) | OWASP LLM05 | High | High | **Critical** | Compromise the system via outdated Python packages (e.g., PyTorch, TensorFlow). |
| [Backdoor Attacks - AI framework](threat-details.md#backdoor-attacks---ai-framework) | STRIDE (Tampering) | Low | Critical | **High** | Exploit hidden vulnerabilities in the AI framework to control agents. |
| [Backdoor Attacks - AI model](threat-details.md#backdoor-attacks---ai-model) | STRIDE (Tampering) | Low | Critical | **High** | Trigger a hidden malicious behavior in the model (e.g., "If input='activate', delete DB"). |
| [Compromised Container Images](threat-details.md#compromised-container-images) | STRIDE (Tampering) | Medium | Critical | **High** | Inject malware into the Docker images running the LLM agents. |
| [Compromised Framework Components](threat-details.md#compromised-framework-components) | OWASP LLM05 | Low | Critical | **High** | Malware inside the AI framework libraries themselves. |
| [Integration Risks](threat-details.md#integration-risks) | OWASP API10 | Medium | High | **High** | Vulnerabilities in SDKs used to connect agents to other systems. |
| [Lateral Movement - AI infrastructure](threat-details.md#lateral-movement---ai-infrastructure) | STRIDE (Elevation) | Medium | High | **High** | Move from a compromised AI component to other sensitive areas of the infrastructure. |
| [Orchestration Attacks](threat-details.md#orchestration-attacks) | STRIDE (Elevation) | Low | Critical | **High** | Exploit Kubernetes/Orchestration flaws to control the AI deployment environment. |
| [Server Side Request Forgery (SSRF)](threat-details.md#server-side-request-forgery-ssrf) | OWASP API | Medium | High | **High** | Abuse the "Application Services" to access internal metadata services or databases. |
| [Supply Chain Attacks - Cross-Layer](threat-details.md#supply-chain-attacks---cross-layer) | OWASP LLM05 | Low | Critical | **High** | A compromise in a lower layer (e.g., OS library) affects higher-level Agent logic. |
| [Compromised Observability Tools](threat-details.md#compromised-observability-tools) | STRIDE (Tampering) | Low | High | **Medium** | Inject code into monitoring tools to hide malicious behavior or exfiltrate logs. |
| [Framework Evasion](threat-details.md#framework-evasion) | STRIDE (Tampering) | Low | High | **Medium** | Agents designed specifically to bypass the security controls of the AI framework. |
| [Lateral Movement - Cross-Layer](threat-details.md#lateral-movement---cross-layer) | STRIDE (Elevation) | Low | High | **Medium** | Move from one logical layer (e.g., Application) to another (e.g., Data). |
| [Poisoning Observability Data](threat-details.md#poisoning-observability-data) | STRIDE (Tampering) | Medium | Medium | **Medium** | Feed false data to monitoring systems to mask attacks or trigger false alarms. |
| [Resource Hijacking](threat-details.md#resource-hijacking) | STRIDE (Tampering) | Medium | Medium | **Medium** | Use the AI infrastructure for unauthorized tasks like cryptomining. |

## API Security & Access Control Threats

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Broken Authentication](threat-details.md#broken-authentication) | OWASP API02 | High | Critical | **Critical** | Hijack user/agent accounts to access data or perform actions on their behalf. |
| [Broken Object Level Authorization](threat-details.md#broken-object-level-authorization) | OWASP API01 | High | Critical | **Critical** | Manipulate IDs to access data belonging to other users (BOLA). |
| [Privilege Escalation](threat-details.md#privilege-escalation) | STRIDE (Elevation) | Medium | Critical | **Critical** | Gain unauthorized privileges in one layer to manipulate others. |
| [Broken Function Level Authorization](threat-details.md#broken-function-level-authorization) | OWASP API05 | Medium | High | **High** | Standard users accessing admin-only API endpoints. |
| [Bypass Access Control](threat-details.md#bypass-access-control) | OWASP API05 | Medium | High | **High** | Circumvent checks via URL tampering or forced browsing. |
| [Improper Inventory Management](threat-details.md#improper-inventory-management) | OWASP API09 | High | Medium | **High** | Attack old/unpatched API versions ("Zombie APIs") to gain access. |
| [Missing authentication](threat-details.md#missing-authentication) | OWASP API02 | Low | High | **High** | Access critical functions without any identity verification. |
| [Security Misconfiguration (API)](threat-details.md#security-misconfiguration-api) | OWASP API08 | High | Medium | **High** | Exploit default settings or unprotected files to compromise the system. |
| [Spoofing](threat-details.md#spoofing) | STRIDE (Spoofing) | Medium | High | **High** | Masquerade as a trusted entity to deceive recipients or gain access. |
| [Unrestricted Resource Consumption](threat-details.md#unrestricted-resource-consumption) | OWASP API04 | High | Medium | **High** | Exhaust system resources via excessive API calls (DoS). |
| [Unsafe Consumption of APIs](threat-details.md#unsafe-consumption-of-apis) | OWASP API10 | Medium | High | **High** | Compromise the system via vulnerabilities in third-party APIs it integrates with. |

## Denial of Service (DoS) Threats

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Denial of Service via Query Flooding](threat-details.md#denial-of-service-via-query-flooding) | STRIDE (DoS) | Medium | High | **High** | Flood the Vector DB with high-dimensional queries to crash the search index. |
| [LLM Denial of Service](threat-details.md#llm-denial-of-service) | OWASP LLM04 | High | Medium | **Medium** | Flood the generation queue to degrade service for legitimate users. |
| [Manipulation of Evaluation Metrics](threat-details.md#manipulation-of-evaluation-metrics) | STRIDE (Tampering) | Low | Medium | **Medium** | Poison benchmarks to make a malicious agent appear effective/safe. |

## Additional threats

| Threat | Framework | Likelihood | Severity | Risk | Attacker goal / impact |
|---|---|---|---|---|---|
| [Broken Object Property Level Authorization](threat-details.md#broken-object-property-level-authorization) |  | n/a | n/a | **Unrated** |  |
| [Cache Poisoning (semantic or vector cache)](threat-details.md#cache-poisoning-semantic-or-vector-cache) |  | n/a | n/a | **Unrated** |  |
| [Denial of Service](threat-details.md#denial-of-service) |  | n/a | n/a | **Unrated** |  |
| [Denial of Service (DoS) Attacks - AI infrastructure](threat-details.md#denial-of-service-dos-attacks---ai-infrastructure) |  | n/a | n/a | **Unrated** |  |
| [Denial of Service (DoS) Attacks - AI model](threat-details.md#denial-of-service-dos-attacks---ai-model) |  | n/a | n/a | **Unrated** |  |
| [Denial of Service on Data Infrastructure](threat-details.md#denial-of-service-on-data-infrastructure) |  | n/a | n/a | **Unrated** |  |
| [Denial of Service on Evaluation Infrastructure](threat-details.md#denial-of-service-on-evaluation-infrastructure) |  | n/a | n/a | **Unrated** |  |
| [Denial of Service on Framework APIs](threat-details.md#denial-of-service-on-framework-apis) |  | n/a | n/a | **Unrated** |  |
| [Elevation of Privilege](threat-details.md#elevation-of-privilege) |  | n/a | n/a | **Unrated** |  |
| [Embedding Inversion / Reconstruction](threat-details.md#embedding-inversion--reconstruction) |  | n/a | n/a | **Unrated** |  |
| [Evasion of Detection](threat-details.md#evasion-of-detection) |  | n/a | n/a | **Unrated** |  |
| [Horizontal/Vertical Solution Vulnerabilities](threat-details.md#horizontalvertical-solution-vulnerabilities) |  | n/a | n/a | **Unrated** |  |
| [Infrastructure-as-Code (IaC) Manipulation](threat-details.md#infrastructure-as-code-iac-manipulation) |  | n/a | n/a | **Unrated** |  |
| [Inject malicious stuff into training process](threat-details.md#inject-malicious-stuff-into-training-process) |  | n/a | n/a | **Unrated** |  |
| [Tampering](threat-details.md#tampering) |  | n/a | n/a | **Unrated** |  |
| [Unauthorized Data Access (Tenant Isolation Failure)](threat-details.md#unauthorized-data-access-tenant-isolation-failure) |  | n/a | n/a | **Unrated** |  |
| [Unrestricted Access to Sensitive Business Flows](threat-details.md#unrestricted-access-to-sensitive-business-flows) |  | n/a | n/a | **Unrated** |  |
