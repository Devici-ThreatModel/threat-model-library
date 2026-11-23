# LLM and Agentic Systems: Threat Details

For each threat: how the attack works, what it affects, and which mitigations counter it. Mitigation names link to the [mitigation library](mitigation-library.md). Back to the [threat list](threats.md) or the [model overview](README.md).

## LLM-Specific & Prompt Injection Threats

### Direct prompt injection

**Priority:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** OWASP LLM01

**Affects:** Application Services

An attacker crafts a direct prompt injection to the LLM, instructing it to ignore the application creator's system prompts and instead execute a prompt that returns private, dangerous, or otherwise undesirable information.

**Attacker goal / impact:** Jailbreak the model to bypass safety guardrails and generate toxic or illegal content.

**Mitigations**

- [Enforce least privilege access for LLMs](mitigation-library.md#enforce-least-privilege-access-for-llms) (Preventive)
- [Implement Trust Boundaries for LLM Interactions](mitigation-library.md#implement-trust-boundaries-for-llm-interactions) (Preventive)
- [Implement user approval for privileged actions](mitigation-library.md#implement-user-approval-for-privileged-actions) (Preventive)
- [Segregate external content from user prompts](mitigation-library.md#segregate-external-content-from-user-prompts) (Preventive)

### Excessive functionality

**Priority:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** OWASP LLM08

**Affects:** Application Services

An attacker accesses plugins which include functions that are not needed via an LLM agent, and the attacker uses those functions to perform a negative action against the system.

**Attacker goal / impact:** Agent has access to plugins/tools it doesn't need, expanding the blast radius of a compromise.

**Mitigations**

- [Limit LLM Plugin Functions](mitigation-library.md#limit-llm-plugin-functions) (Preventive)
- [Limit plugin functionality](mitigation-library.md#limit-plugin-functionality) (Preventive)
- [Restrict plugin access](mitigation-library.md#restrict-plugin-access) (Preventive)

### Indirect prompt injection

**Priority:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** OWASP LLM01

**Affects:** LLM Model, Application Services

An attacker uploads a document containing an indirect prompt injection.

**Attacker goal / impact:** Compromise the model via untrusted external data (e.g., a malicious website) to manipulate subsequent user interactions.

**Mitigations**

- [Enforce least privilege access for LLMs](mitigation-library.md#enforce-least-privilege-access-for-llms) (Preventive)
- [Implement Trust Boundaries for LLM Interactions](mitigation-library.md#implement-trust-boundaries-for-llm-interactions) (Preventive)
- [Implement user approval for privileged actions](mitigation-library.md#implement-user-approval-for-privileged-actions) (Preventive)
- [Segregate external content from user prompts](mitigation-library.md#segregate-external-content-from-user-prompts) (Preventive)

### LLM Chain Injection

**Priority:** Critical · **Likelihood:** Medium · **Severity:** Critical · **Framework:** OWASP LLM01

**Affects:** RAG private data stores

If RAG pipeline uses “tool calling,” attacker injects tool-use commands.

**Attacker goal / impact:** Inject malicious tool-use commands into the RAG pipeline to force the agent to execute unsafe actions.

**Mitigations**

- [Instruction Isolation with Guardrail Mediation Layer](mitigation-library.md#instruction-isolation-with-guardrail-mediation-layer) (Preventive)
- [Tool-Use Policy Enforcement and Schema-Validated Arguments](mitigation-library.md#tool-use-policy-enforcement-and-schema-validated-arguments) (Preventive)

### Command Execution for LLM

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** OWASP LLM02

**Affects:** Application Services

LLM output is entered directly into a system shell or similar function such as exec or eval; an attacker is able to cause this to happen, resulting in remote code execution.

**Attacker goal / impact:** Achieve Remote Code Execution (RCE) by tricking the LLM into generating code that is passed to exec() or eval().

**Mitigations**

- [Sanitize Output](mitigation-library.md#sanitize-output) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Excessive autonomy

**Priority:** High · **Likelihood:** Medium · **Severity:** Critical · **Framework:** OWASP LLM08

**Affects:** LLM Model, Application Services

An LLM-based application or plugin fails to verify and approve high-impact actions independently.

**Attacker goal / impact:** Agent takes high-impact actions (e.g., deleting data, sending emails) without human approval.

**Mitigations**

- [Implement Downstream Authorization Checks](mitigation-library.md#implement-downstream-authorization-checks) (Preventive)
- [Implement human approval for high-impact actions](mitigation-library.md#implement-human-approval-for-high-impact-actions) (Preventive)
- [Implement user approval for privileged actions](mitigation-library.md#implement-user-approval-for-privileged-actions) (Preventive)

### Inaccurate LLM information

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** OWASP LLM09

**Affects:** Application Services

LLM provides inaccurate information as a response while stating it in a fashion implying it is highly authoritative. The overall system is designed without proper checks and balances to handle this, and the information misleads the user in a way that leads to harm.

**Attacker goal / impact:** Generate "Hallucinations" that mislead users, causing reputational damage or safety issues.

**Mitigations**

- [Fine-tune the LLM for accuracy](mitigation-library.md#fine-tune-the-llm-for-accuracy) (Preventive)
- [Review LLM Outputs Regularly](mitigation-library.md#review-llm-outputs-regularly) (Detective)
- [Validate LLM responses with trusted sources](mitigation-library.md#validate-llm-responses-with-trusted-sources) (Preventive)

### Rogue LLM Instructions

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** OWASP LLM01

**Affects:** Application Services

An attacker uses rogue instructions and content embedded in a visited website to exploit and scam users.

**Attacker goal / impact:** Scam users by embedding hidden instructions in web content that the LLM processes and presents as truth.

**Mitigations**

- [Enforce least privilege access for LLMs](mitigation-library.md#enforce-least-privilege-access-for-llms) (Preventive)
- [Implement Trust Boundaries for LLM Interactions](mitigation-library.md#implement-trust-boundaries-for-llm-interactions) (Preventive)
- [Implement user approval for privileged actions](mitigation-library.md#implement-user-approval-for-privileged-actions) (Preventive)
- [Segregate external content from user prompts](mitigation-library.md#segregate-external-content-from-user-prompts) (Preventive)

### User-driven prompt injection

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP LLM01

**Affects:** Application Services

A user employs an LLM to summarize a webpage containing an indirect prompt injection. This then causes the LLM to solicit sensitive information from the user and perform exfiltration via JavaScript or Markdown.

**Attacker goal / impact:** Trick the user into summarizing a malicious document, leading to data exfiltration via the user's browser.

**Mitigations**

- [Enforce least privilege access for LLMs](mitigation-library.md#enforce-least-privilege-access-for-llms) (Preventive)
- [Implement Trust Boundaries for LLM Interactions](mitigation-library.md#implement-trust-boundaries-for-llm-interactions) (Preventive)
- [Implement user approval for privileged actions](mitigation-library.md#implement-user-approval-for-privileged-actions) (Preventive)
- [Segregate external content from user prompts](mitigation-library.md#segregate-external-content-from-user-prompts) (Preventive)

### XSS by LLM

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP LLM02

**Affects:** Application Services

JavaScript or Markdown is generated by the LLM and returned to a user. The code is then interpreted by the browser, resulting in XSS.

**Attacker goal / impact:** Generate malicious JavaScript/Markdown that executes in the user's browser (Cross-Site Scripting).

**Mitigations**

- [Sanitize Output](mitigation-library.md#sanitize-output) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Adversarial Examples

**Priority:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents), Application Services

Inputs specifically crafted to fool the AI model into making incorrect predictions or behave in unexpected ways, causing instability or incorrect responses from the AI.

**Attacker goal / impact:** Destabilize the model with crafted inputs to force incorrect classifications or responses.

**Mitigations**

- [Alert on skewed LLM responses](mitigation-library.md#alert-on-skewed-llm-responses) (Detective)
- [Review LLM Outputs Regularly](mitigation-library.md#review-llm-outputs-regularly) (Detective)
- [Validate LLM responses with trusted sources](mitigation-library.md#validate-llm-responses-with-trusted-sources) (Preventive)

### Reprogramming Attacks

**Priority:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents), Fine-tuning data, Training data, Application Services

Repurposing the AI model for a malicious task different from its original intent, manipulating the model for unexpected and harmful uses.

**Attacker goal / impact:** Repurpose the model for tasks it wasn't designed for (e.g., using a chatbot for spam).

**Mitigations**

- [Enforce usage policy and detect unauthorized fine-tuning](mitigation-library.md#enforce-usage-policy-and-detect-unauthorized-fine-tuning) (Preventive)
- [Establish alignment verification gates for agent outputs](mitigation-library.md#establish-alignment-verification-gates-for-agent-outputs) (Preventive)
- [Implement Trust Boundaries for LLM Interactions](mitigation-library.md#implement-trust-boundaries-for-llm-interactions) (Preventive)
- [Protect AI agents from goal manipulation](mitigation-library.md#protect-ai-agents-from-goal-manipulation) (Preventive)

## Agent & Goal Manipulation Threats

### Agent Impersonation

**Priority:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** STRIDE (Spoofing)

**Affects:** LLM Automation (Agents)

Malicious actors deceiving users or other agents by impersonating legitimate AI agents within the ecosystem.

**Attacker goal / impact:** A malicious actor poses as a legitimate agent to deceive users or other agents.

**Mitigations**

- [Apply access and privilege management for AI agents](mitigation-library.md#apply-access-and-privilege-management-for-ai-agents) (Preventive)
- [Establish agent identity and trust verification](mitigation-library.md#establish-agent-identity-and-trust-verification) (Preventive)
- [Establish governance and auditability for AI agents](mitigation-library.md#establish-governance-and-auditability-for-ai-agents) (Detective)
- [Make agent identity visible and verifiable](mitigation-library.md#make-agent-identity-visible-and-verifiable) (Preventive)

### Agent Tool Misuse

**Priority:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** OWASP LLM01

**Affects:** LLM Automation (Agents)

AI agents being manipulated to utilize their tools in ways not intended, leading to unforeseen and potentially harmful actions within the system.

**Attacker goal / impact:** Manipulate an agent to use its connected tools (e.g., email, code exec) harmfully.

**Mitigations**

- [Apply access and privilege management for AI agents](mitigation-library.md#apply-access-and-privilege-management-for-ai-agents) (Preventive)
- [Establish governance and auditability for AI agents](mitigation-library.md#establish-governance-and-auditability-for-ai-agents) (Detective)
- [Implement behavioral monitoring and anomaly detection for AI agents](mitigation-library.md#implement-behavioral-monitoring-and-anomaly-detection-for-ai-agents) (Detective)
- [Prevent misuse of tools by AI agents](mitigation-library.md#prevent-misuse-of-tools-by-ai-agents) (Preventive)

### Agent Goal Manipulation

**Priority:** High · **Likelihood:** Medium · **Severity:** Critical · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents), Application Services

Attackers manipulating the intended goals of AI agents, causing them to pursue objectives different from their original purpose or be detrimental to the environment.

**Attacker goal / impact:** Force agents to pursue malicious objectives (e.g., "Ignore safety, maximize clicks").

**Mitigations**

- [Protect AI agents from goal manipulation](mitigation-library.md#protect-ai-agents-from-goal-manipulation) (Preventive)

### Agent Identity Attack

**Priority:** High · **Likelihood:** Medium · **Severity:** Critical · **Framework:** STRIDE (Spoofing)

**Affects:** LLM Automation (Agents)

Attacks that compromise the identity and authorization mechanisms of AI agents in the ecosystem, resulting in unauthorized access and control of the agent.

**Attacker goal / impact:** Compromise agent auth mechanisms to gain unauthorized control of the agent.

**Mitigations**

- [Apply access and privilege management for AI agents](mitigation-library.md#apply-access-and-privilege-management-for-ai-agents) (Preventive)
- [Establish agent identity and trust verification](mitigation-library.md#establish-agent-identity-and-trust-verification) (Preventive)
- [Establish governance and auditability for AI agents](mitigation-library.md#establish-governance-and-auditability-for-ai-agents) (Detective)
- [Harden identity and authorization mechanisms for AI agents](mitigation-library.md#harden-identity-and-authorization-mechanisms-for-ai-agents) (Preventive)

### Bias in Security AI Agents

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** STRIDE (Tampering)

**Affects:** Fine-tuning data, Training data

Biases in AI security agents that lead to unfair or discriminatory security practices, where certain systems are not adequately protected.

**Attacker goal / impact:** Security agents learn biases that cause them to ignore certain threats or flag innocent users.

**Mitigations**

- [Detect and mitigate bias in security AI agents](mitigation-library.md#detect-and-mitigate-bias-in-security-ai-agents) (Detective)

### Compromised Agents

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents)

Malicious AI agents designed to perform harmful actions, infiltrating the ecosystem by posing as legitimate services.

**Attacker goal / impact:** Malicious agents infiltrate the ecosystem, acting as legitimate services to harm others.

**Mitigations**

- [Apply access and privilege management for AI agents](mitigation-library.md#apply-access-and-privilege-management-for-ai-agents) (Preventive)
- [Enforce code integrity and supply chain security for AI agents](mitigation-library.md#enforce-code-integrity-and-supply-chain-security-for-ai-agents) (Preventive)
- [Establish agent identity and trust verification](mitigation-library.md#establish-agent-identity-and-trust-verification) (Preventive)
- [Establish governance and auditability for AI agents](mitigation-library.md#establish-governance-and-auditability-for-ai-agents) (Detective)
- [Implement behavioral monitoring and anomaly detection for AI agents](mitigation-library.md#implement-behavioral-monitoring-and-anomaly-detection-for-ai-agents) (Detective)

### Goal Misalignment Cascades

**Priority:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents), Fine-tuning data, Training data

Goal misalignment in one agent (e.g., due to data poisoning in Layer 2) that can propagate to other agents through interactions in the Agent Ecosystem.

**Attacker goal / impact:** Malicious goal changes in one agent propagate to others, destabilizing the ecosystem.

**Mitigations**

- [Establish alignment verification gates for agent outputs](mitigation-library.md#establish-alignment-verification-gates-for-agent-outputs) (Preventive)
- [Implement behavioral monitoring and anomaly detection for AI agents](mitigation-library.md#implement-behavioral-monitoring-and-anomaly-detection-for-ai-agents) (Detective)
- [Implement human approval for high-impact actions](mitigation-library.md#implement-human-approval-for-high-impact-actions) (Preventive)
- [Protect AI agents from goal manipulation](mitigation-library.md#protect-ai-agents-from-goal-manipulation) (Preventive)
- [Test cross-agent interactions with sandboxing and adversarial simulations](mitigation-library.md#test-cross-agent-interactions-with-sandboxing-and-adversarial-simulations) (Detective)

### Repudiation - AI agent

**Priority:** Medium · **Likelihood:** High · **Severity:** Low · **Framework:** STRIDE (Repudiation)

**Affects:** LLM Automation (Agents)

AI agents denying actions they performed, creating accountability issues in the system due to the difficulty in tracing actions back to an AI agent.

**Attacker goal / impact:** Agents deny actions they performed, complicating accountability and forensics.

**Mitigations**

- [Ensure accountability for AI agents](mitigation-library.md#ensure-accountability-for-ai-agents) (Detective)

### Repudiation

**Priority:** Low · **Likelihood:** Medium · **Severity:** Low · **Framework:** STRIDE (Repudiation)

**Affects:** Server-side functions, Application Services

Repudiation is the rejection or denial of a performed action.

**Attacker goal / impact:** Generic denial of performed actions by users or system components.

**Mitigations**

- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Log Security Events](mitigation-library.md#log-security-events) (Detective)

## Data Integrity & Poisoning Threats

### Compromised RAG Pipelines

**Priority:** High · **Likelihood:** Medium · **Severity:** Critical · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents), Training data

Injecting malicious code or data into AI data processing workflows, causing erroneous results or malicious AI agent behavior.

**Attacker goal / impact:** Inject malicious code/data into the RAG workflow, causing erroneous or harmful agent behavior.

**Mitigations**

- [Implement data sanitization techniques](mitigation-library.md#implement-data-sanitization-techniques) (Preventive)
- [Implement Data Version Control](mitigation-library.md#implement-data-version-control) (Corrective)
- [Protect RAG pipelines](mitigation-library.md#protect-rag-pipelines) (Preventive)

### Data Poisoning - AI Agent

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents), Fine-tuning data, Training data

Manipulating training data to compromise AI agent behavior, leading to biased results or unintended consequences in AI decision making.

**Attacker goal / impact:** Manipulate operational data to bias agent decisions in real-time.

**Mitigations**

- [Implement data sanitization techniques](mitigation-library.md#implement-data-sanitization-techniques) (Preventive)
- [Implement Data Version Control](mitigation-library.md#implement-data-version-control) (Corrective)
- [Implement hashing for data integrity verification.](mitigation-library.md#implement-hashing-for-data-integrity-verification) (Detective)
- [Implement robust sandboxing measures](mitigation-library.md#implement-robust-sandboxing-measures) (Preventive)
- [Verify data source legitimacy](mitigation-library.md#verify-data-source-legitimacy) (Preventive)
- [Verify Training Data Sources](mitigation-library.md#verify-training-data-sources) (Preventive)

### Data Poisoning - Training Phase

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** OWASP LLM03

**Affects:** LLM Automation (Agents), Fine-tuning data, Training data, Vector DB, RAG private data stores

Injecting malicious data into the AI model's training set to compromise its behavior, resulting in skewed or biased model behavior in AI systems.

**Attacker goal / impact:** Inject malicious samples into the "Training dataset" to permanently compromise model behavior/safety.

**Mitigations**

- [Alert on skewed LLM responses](mitigation-library.md#alert-on-skewed-llm-responses) (Detective)
- [Fine-tune the LLM for accuracy](mitigation-library.md#fine-tune-the-llm-for-accuracy) (Preventive)
- [Implement data sanitization techniques](mitigation-library.md#implement-data-sanitization-techniques) (Preventive)
- [Review LLM Outputs Regularly](mitigation-library.md#review-llm-outputs-regularly) (Detective)
- [Verify Training Data Sources](mitigation-library.md#verify-training-data-sources) (Preventive)

### Index Poisoning

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** STRIDE (Tampering)

**Affects:** Vector DB

Insertion of crafted vectors that cluster near sensitive ones, hijacking similarity search.

**Attacker goal / impact:** Insert crafted vectors into the "Vector DB" to hijack search results and surface malicious context.

**Mitigations**

- [Anomaly Detection and Segmentation of High-Sensitivity Vectors](mitigation-library.md#anomaly-detection-and-segmentation-of-high-sensitivity-vectors) (Detective)
- [Trust-Scoped Ingestion and Embedding Validation](mitigation-library.md#trust-scoped-ingestion-and-embedding-validation) (Preventive)

### Model Drift via Reindexing

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** STRIDE (Tampering)

**Affects:** RAG private data stores

Reindexing pipelines inadvertently ingest unvetted or poisoned sources.

**Attacker goal / impact:** RAG pipeline accidentally ingests unvetted/poisoned sources during automated updates.

**Mitigations**

- [Controlled Reindexing Pipelines with Source Validation](mitigation-library.md#controlled-reindexing-pipelines-with-source-validation) (Preventive)
- [Staged Reindexing with Audit and Approval Gates](mitigation-library.md#staged-reindexing-with-audit-and-approval-gates) (Preventive)

### RAG Supply Chain Poisoning

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** OWASP LLM05

**Affects:** RAG private data stores

Manipulating open-source retriever libraries (LangChain, LlamaIndex) to exfiltrate retrievals.

**Attacker goal / impact:** Compromise open-source libraries (LangChain/LlamaIndex) to steal retrieved data.

**Mitigations**

- [Network Egress Control and Data Minimization for Retriever Components](mitigation-library.md#network-egress-control-and-data-minimization-for-retriever-components) (Preventive)
- [Vendor-Pinned, Reviewed, and Monitored Retriever Dependencies](mitigation-library.md#vendor-pinned-reviewed-and-monitored-retriever-dependencies) (Preventive)

### Security Agent Data Poisoning

**Priority:** High · **Likelihood:** Medium · **Severity:** Critical · **Framework:** STRIDE (Tampering)

**Affects:** Fine-tuning data, Training data

Attackers manipulating the training or operational data used by AI security agents, causing them to misidentify threats or generate false positives, impacting the AI security process.

**Attacker goal / impact:** Manipulate data used by security agents so they misidentify threats.

**Mitigations**

- [Implement behavioral monitoring and anomaly detection for AI agents](mitigation-library.md#implement-behavioral-monitoring-and-anomaly-detection-for-ai-agents) (Detective)
- [Implement data sanitization techniques](mitigation-library.md#implement-data-sanitization-techniques) (Preventive)
- [Implement robust sandboxing measures](mitigation-library.md#implement-robust-sandboxing-measures) (Preventive)
- [Verify Training Data Sources](mitigation-library.md#verify-training-data-sources) (Preventive)

### Data Tampering

**Priority:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents)

Modifying AI data in transit or at rest, leading to incorrect agent behavior or inaccurate results within AI systems.

**Attacker goal / impact:** Modify AI data in transit between the Application Services and the Model.

**Mitigations**

- [Implement data sanitization techniques](mitigation-library.md#implement-data-sanitization-techniques) (Preventive)
- [Implement Data Version Control](mitigation-library.md#implement-data-version-control) (Corrective)
- [Implement hashing for data integrity verification.](mitigation-library.md#implement-hashing-for-data-integrity-verification) (Detective)
- [Verify data source legitimacy](mitigation-library.md#verify-data-source-legitimacy) (Preventive)
- [Verify Training Data Sources](mitigation-library.md#verify-training-data-sources) (Preventive)

### Malicious pre-training

**Priority:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** OWASP LLM03

**Affects:** LLM Model, Training data

A malicious actor or a competitor brand intentionally creates inaccurate or malicious documents targeted at a model's pre-training, fine-tuning data, or embeddings.

**Attacker goal / impact:** A competitor intentionally seeds public data with malicious documents to sabotage the model.

**Mitigations**

- [Alert on skewed LLM responses](mitigation-library.md#alert-on-skewed-llm-responses) (Detective)
- [Architect distinct LLMs for specific use cases.](mitigation-library.md#architect-distinct-llms-for-specific-use-cases) (Preventive)
- [Implement Data Version Control](mitigation-library.md#implement-data-version-control) (Corrective)
- [Implement robust sandboxing measures](mitigation-library.md#implement-robust-sandboxing-measures) (Preventive)
- [Implement User-Supplied Info in Vector Database](mitigation-library.md#implement-user-supplied-info-in-vector-database) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)
- [Verify data source legitimacy](mitigation-library.md#verify-data-source-legitimacy) (Preventive)
- [Verify Training Data Sources](mitigation-library.md#verify-training-data-sources) (Preventive)

## Privacy, Extraction & Tenant Isolation Threats

### Data Exfiltration

**Priority:** Critical · **Likelihood:** Medium · **Severity:** Critical · **Framework:** LINDDUN (Disclosure)

**Affects:** LLM Automation (Agents)

Stealing sensitive AI data stored in databases or data stores, exposing private and confidential information related to AI systems.

**Attacker goal / impact:** Steal sensitive AI training data or user logs from databases.

**Mitigations**

- [Apply access and privilege management for AI agents](mitigation-library.md#apply-access-and-privilege-management-for-ai-agents) (Preventive)
- [Detect and respond to AI data exfiltration attempts](mitigation-library.md#detect-and-respond-to-ai-data-exfiltration-attempts) (Detective)
- [Establish governance and auditability for AI agents](mitigation-library.md#establish-governance-and-auditability-for-ai-agents) (Detective)
- [Implement behavioral monitoring and anomaly detection for AI agents](mitigation-library.md#implement-behavioral-monitoring-and-anomaly-detection-for-ai-agents) (Detective)
- [Implement robust sandboxing measures](mitigation-library.md#implement-robust-sandboxing-measures) (Preventive)
- [Implement strict compartmentalization of safe areas](mitigation-library.md#implement-strict-compartmentalization-of-safe-areas) (Preventive)

### Data Leakage

**Priority:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** LINDDUN (Disclosure)

**Affects:** LLM Automation (Agents), Vector DB, RAG private data stores

Sensitive data from one layer being exposed through another layer.

**Attacker goal / impact:** Sensitive data from one layer exposed through another.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Enforce Control/Data Plane Separation](mitigation-library.md#enforce-controldata-plane-separation) (Preventive)
- [Implement access control mechanisms](mitigation-library.md#implement-access-control-mechanisms) (Preventive)
- [Implement schema-based response validation](mitigation-library.md#implement-schema-based-response-validation) (Preventive)
- [Limit property exposure](mitigation-library.md#limit-property-exposure) (Preventive)

### Data Leakage through Observability

**Priority:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** LINDDUN (Disclosure)

**Affects:** LLM Automation (Agents)

Sensitive AI information inadvertently exposed through logs or monitoring dashboards, due to misconfiguration, creating privacy and confidentiality risks.

**Attacker goal / impact:** Sensitive data (PII, API keys) is inadvertently logged and exposed via dashboards.

**Mitigations**

- [Establish governance and auditability for AI agents](mitigation-library.md#establish-governance-and-auditability-for-ai-agents) (Detective)
- [Protect the integrity of observability tools monitoring AI agents](mitigation-library.md#protect-the-integrity-of-observability-tools-monitoring-ai-agents) (Preventive)

### Improper Data Retention / Deletion

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** LINDDUN (Compliance)

**Affects:** Vector DB

Embeddings remain after the original data is deleted or access is revoked.

**Attacker goal / impact:** Embeddings remain in the Vector DB after the original document is deleted.

**Mitigations**

- [Linked Deletion Workflows for Source and Embeddings](mitigation-library.md#linked-deletion-workflows-for-source-and-embeddings) (Corrective)
- [Retention-Aware Index Management and Periodic Reconciliation](mitigation-library.md#retention-aware-index-management-and-periodic-reconciliation) (Detective)

### Information Disclosure

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** STRIDE (Disclosure)

**Affects:** Server-side functions, Application Services

Information disclosure is the unintentional exposure or release of confidential or sensitive data to unauthorized individuals or entities.

**Attacker goal / impact:** Unintentional release of confidential data to unauthorized parties.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Model Stealing

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP LLM10

**Affects:** LLM Automation (Agents)

Attackers extracting a copy of the AI model through API queries for use in a different application, resulting in IP theft or competitive disadvantage specifically related to AI.

**Attacker goal / impact:** Extract the model's weights or functional equivalent via API query patterns.

**Mitigations**

- [Apply access and privilege management for AI agents](mitigation-library.md#apply-access-and-privilege-management-for-ai-agents) (Preventive)
- [Enforce least privilege access for LLMs](mitigation-library.md#enforce-least-privilege-access-for-llms) (Preventive)
- [Harden identity and authorization mechanisms for AI agents](mitigation-library.md#harden-identity-and-authorization-mechanisms-for-ai-agents) (Preventive)
- [Implement API rate limiting](mitigation-library.md#implement-api-rate-limiting) (Preventive)
- [Implement behavioral monitoring and anomaly detection for AI agents](mitigation-library.md#implement-behavioral-monitoring-and-anomaly-detection-for-ai-agents) (Detective)
- [Implement Trust Boundaries for LLM Interactions](mitigation-library.md#implement-trust-boundaries-for-llm-interactions) (Preventive)
- [Limit LLM Plugin Functions](mitigation-library.md#limit-llm-plugin-functions) (Preventive)
- [Restrict LLM Plugin Permissions](mitigation-library.md#restrict-llm-plugin-permissions) (Preventive)
- [Restrict plugin access](mitigation-library.md#restrict-plugin-access) (Preventive)

### Model theft

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE (Tampering)

**Affects:** LLM Model, Application Services

Malicious actors or APTs access and exfiltrate the LLM model.

**Attacker goal / impact:** Direct theft of the model file from the server/container.

**Mitigations**

- [Implement extreme least privilege access controls](mitigation-library.md#implement-extreme-least-privilege-access-controls) (Preventive)
- [Implement Role-Based Access Control (RBAC)](mitigation-library.md#implement-role-based-access-control-rbac) (Preventive)

### Tenant Boundary Violation

**Priority:** High · **Likelihood:** Medium · **Severity:** Critical · **Framework:** LINDDUN (Disclosure)

**Affects:** RAG private data stores

Poor isolation in multi-tenant vector stores allows cross-index queries.

**Attacker goal / impact:** Poor isolation allows one tenant to query another's data in vector stores.

**Mitigations**

- [Physically and Logically Isolated Tenant Indexes](mitigation-library.md#physically-and-logically-isolated-tenant-indexes) (Preventive)
- [Tenant-Scoped Query Enforcement and Policy Controls](mitigation-library.md#tenant-scoped-query-enforcement-and-policy-controls) (Preventive)

### User data bleed over

**Priority:** High · **Likelihood:** Medium · **Severity:** Critical · **Framework:** LINDDUN (Disclosure)

**Affects:** Fine-tuning data, Training data, Application Services

Unsuspecting legitimate user A is exposed to specific other user data via the LLM when interacting with the LLM application in a non-malicious manner.

**Attacker goal / impact:** One user sees another user's private data in the LLM response (Cross-Tenant Leak).

**Mitigations**

- [Implement data sanitization techniques](mitigation-library.md#implement-data-sanitization-techniques) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Membership Inference Attacks

**Priority:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** LINDDUN (Disclosure)

**Affects:** LLM Automation (Agents), Fine-tuning data, Training data, Application Services

Determining whether a specific data point was used to train the AI model, potentially revealing private information or violating confidentiality of the training data.

**Attacker goal / impact:** Determine if a specific user's data was used to train the model.

**Mitigations**

- [Enforce least privilege access for LLMs](mitigation-library.md#enforce-least-privilege-access-for-llms) (Preventive)
- [Implement Role-Based Access Control (RBAC)](mitigation-library.md#implement-role-based-access-control-rbac) (Preventive)
- [Implement Trust Boundaries for LLM Interactions](mitigation-library.md#implement-trust-boundaries-for-llm-interactions) (Preventive)
- [Prevent overfitting and memorization during training](mitigation-library.md#prevent-overfitting-and-memorization-during-training) (Preventive)
- [Restrict sensitive outputs and queries at runtime](mitigation-library.md#restrict-sensitive-outputs-and-queries-at-runtime) (Preventive)

### Metadata leakage

**Priority:** Medium · **Likelihood:** High · **Severity:** Low · **Framework:** LINDDUN (Disclosure)

**Affects:** RAG private data stores

Retrievers return metadata (paths, owners, timestamps) revealing structure of private data.

**Attacker goal / impact:** Retriever returns file paths or owner names, revealing internal infrastructure.

**Mitigations**

- [Apply Fine-Grained Access Controls and Contextual Authorization for Metadata Exposure](mitigation-library.md#apply-fine-grained-access-controls-and-contextual-authorization-for-metadata-exposure) (Preventive)
- [Enforce Metadata-Stripping and Schema-Controlled Retrieval Outputs](mitigation-library.md#enforce-metadata-stripping-and-schema-controlled-retrieval-outputs) (Preventive)

### Retrieval Side-Channel Attack

**Priority:** Low · **Likelihood:** Low · **Severity:** Low · **Framework:** LINDDUN (Disclosure)

**Affects:** RAG private data stores

Timing or similarity scoring reveals hints about corpus contents.

**Attacker goal / impact:** Analyze timing/latency of RAG retrievals to guess the contents of the private corpus.

**Mitigations**

- [Response Normalization and Score Obfuscation](mitigation-library.md#response-normalization-and-score-obfuscation) (Preventive)
- [Strict Query-Context Authorization and Result-Scope Limiting](mitigation-library.md#strict-query-context-authorization-and-result-scope-limiting) (Preventive)

## Supply Chain & Infrastructure Integrity Threats

### Input Validation Attacks

**Priority:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents)

Exploiting weaknesses in how the AI framework handles user inputs, allowing for code injection and potential system compromise of AI agent systems.

**Attacker goal / impact:** Inject malicious code via weak input handling in the AI framework.

**Mitigations**

- [Review code to eliminate code injection vulnerabilities](mitigation-library.md#review-code-to-eliminate-code-injection-vulnerabilities) (Detective)
- [Sanitize Output](mitigation-library.md#sanitize-output) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Supply Chain Attacks

**Priority:** Critical · **Likelihood:** Medium · **Severity:** Critical · **Framework:** OWASP LLM05

**Affects:** LLM Automation (Agents)

Targeting the AI framework’s dependencies, compromising software before delivery and distribution, resulting in compromised AI agent software.

**Attacker goal / impact:** Compromise dependencies (libraries, models) before they are deployed.

**Mitigations**

- [Conduct Software Composition Analysis](mitigation-library.md#conduct-software-composition-analysis) (Detective)
- [Enforce code integrity and supply chain security for AI agents](mitigation-library.md#enforce-code-integrity-and-supply-chain-security-for-ai-agents) (Preventive)
- [Implement secondary review for uploaded artifacts](mitigation-library.md#implement-secondary-review-for-uploaded-artifacts) (Detective)
- [Utilize trusted repositories for libraries and dependencies](mitigation-library.md#utilize-trusted-repositories-for-libraries-and-dependencies) (Preventive)

### Supply Chain LLM Issues

**Priority:** Critical · **Likelihood:** High · **Severity:** High · **Framework:** OWASP LLM05

**Affects:** LLM Model

An attacker uses traditional third-party package vulnerabilities, including outdated or deprecated components.

**Attacker goal / impact:** Compromise the system via outdated Python packages (e.g., PyTorch, TensorFlow).

**Mitigations**

- [Implement Timely Patching](mitigation-library.md#implement-timely-patching) (Preventive)

### Backdoor Attacks - AI framework

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents)

Hidden vulnerabilities or functionalities in the AI framework, exploited by attackers to gain unauthorized access and control over AI agents.

**Attacker goal / impact:** Exploit hidden vulnerabilities in the AI framework to control agents.

**Mitigations**

- [Conduct Software Composition Analysis](mitigation-library.md#conduct-software-composition-analysis) (Detective)
- [Detect and prevent backdoors in AI frameworks](mitigation-library.md#detect-and-prevent-backdoors-in-ai-frameworks) (Preventive)
- [Implement secondary review for uploaded artifacts](mitigation-library.md#implement-secondary-review-for-uploaded-artifacts) (Detective)
- [Secure security agent control plane and runtime attestation](mitigation-library.md#secure-security-agent-control-plane-and-runtime-attestation) (Preventive)
- [Utilize trusted repositories for libraries and dependencies](mitigation-library.md#utilize-trusted-repositories-for-libraries-and-dependencies) (Preventive)

### Backdoor Attacks - AI model

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents)

Hidden triggers within the AI model that cause it to behave in a specific way when activated, usually malicious, leading to unpredictable and potentially harmful behavior from the AI model.

**Attacker goal / impact:** Trigger a hidden malicious behavior in the model (e.g., "If input='activate', delete DB").

**Mitigations**

- [Detect backdoors during model acquisition, training, and validation](mitigation-library.md#detect-backdoors-during-model-acquisition-training-and-validation) (Detective)
- [Enforce SBOM for AI supply chain security](mitigation-library.md#enforce-sbom-for-ai-supply-chain-security) (Preventive)
- [Establish alignment verification gates for agent outputs](mitigation-library.md#establish-alignment-verification-gates-for-agent-outputs) (Preventive)
- [Implement secondary review for uploaded artifacts](mitigation-library.md#implement-secondary-review-for-uploaded-artifacts) (Detective)
- [Neutralize and contain backdoors during deployment and runtime](mitigation-library.md#neutralize-and-contain-backdoors-during-deployment-and-runtime) (Corrective)
- [Utilize trusted repositories for libraries and dependencies](mitigation-library.md#utilize-trusted-repositories-for-libraries-and-dependencies) (Preventive)

### Compromised Container Images

**Priority:** High · **Likelihood:** Medium · **Severity:** Critical · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents)

Malicious code injected into AI agent containers that can infect production systems, compromising the AI deployment environment.

**Attacker goal / impact:** Inject malware into the Docker images running the LLM agents.

**Mitigations**

- [Monitor production code for drift](mitigation-library.md#monitor-production-code-for-drift) (Detective)
- [Source trusted libraries and packages](mitigation-library.md#source-trusted-libraries-and-packages) (Preventive)
- [Utilize trusted repositories for libraries and dependencies](mitigation-library.md#utilize-trusted-repositories-for-libraries-and-dependencies) (Preventive)

### Compromised Framework Components

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** OWASP LLM05

**Affects:** LLM Automation (Agents)

Malicious code in libraries or modules used by AI frameworks, compromising the functionality of the framework and leading to unexpected results.

**Attacker goal / impact:** Malware inside the AI framework libraries themselves.

**Mitigations**

- [Conduct Software Composition Analysis](mitigation-library.md#conduct-software-composition-analysis) (Detective)
- [Implement secondary review for uploaded artifacts](mitigation-library.md#implement-secondary-review-for-uploaded-artifacts) (Detective)
- [Utilize trusted repositories for libraries and dependencies](mitigation-library.md#utilize-trusted-repositories-for-libraries-and-dependencies) (Preventive)

### Integration Risks

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP API10

**Affects:** LLM Automation (Agents)

Vulnerabilities or weaknesses in APIs or SDKs used to integrate AI agents with other systems, resulting in compromised interactions and wider security issues.

**Attacker goal / impact:** Vulnerabilities in SDKs used to connect agents to other systems.

**Mitigations**

- [Secure integrations of AI agents with external systems](mitigation-library.md#secure-integrations-of-ai-agents-with-external-systems) (Preventive)

### Lateral Movement - AI infrastructure

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** STRIDE (Elevation)

**Affects:** LLM Automation (Agents)

Attackers gaining access to one part of the AI infrastructure and then using that access to compromise other sensitive AI areas, compromising additional systems and data in the AI ecosystem.

**Attacker goal / impact:** Move from a compromised AI component to other sensitive areas of the infrastructure.

**Mitigations**

- [Apply access and privilege management for AI agents](mitigation-library.md#apply-access-and-privilege-management-for-ai-agents) (Preventive)
- [Detect and prevent lateral movement in AI infrastructure](mitigation-library.md#detect-and-prevent-lateral-movement-in-ai-infrastructure) (Preventive)
- [Implement behavioral monitoring and anomaly detection for AI agents](mitigation-library.md#implement-behavioral-monitoring-and-anomaly-detection-for-ai-agents) (Detective)
- [Implement Distributed Architecture](mitigation-library.md#implement-distributed-architecture) (Preventive)
- [Implement strict compartmentalization of safe areas](mitigation-library.md#implement-strict-compartmentalization-of-safe-areas) (Preventive)
- [Secure integrations of AI agents with external systems](mitigation-library.md#secure-integrations-of-ai-agents-with-external-systems) (Preventive)

### Orchestration Attacks

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** STRIDE (Elevation)

**Affects:** LLM Automation (Agents)

Exploiting vulnerabilities in systems like Kubernetes to gain unauthorized access and control over AI deployment systems, disrupting AI agent functionality.

**Attacker goal / impact:** Exploit Kubernetes/Orchestration flaws to control the AI deployment environment.

**Mitigations**

- [Automate configuration assessments](mitigation-library.md#automate-configuration-assessments) (Detective)
- [Harden and monitor orchestration platforms for AI agents](mitigation-library.md#harden-and-monitor-orchestration-platforms-for-ai-agents) (Preventive)
- [Update configurations regularly](mitigation-library.md#update-configurations-regularly) (Preventive)

### Server Side Request Forgery (SSRF)

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP API

**Affects:** Server-side functions, Application Services

Attackers could exploit SSRF vulnerabilities in APIs to cause internal services enumeration, information disclosure, bypassing firewalls, or server misuse.

**Attacker goal / impact:** Abuse the "Application Services" to access internal metadata services or databases.

**Mitigations**

- [Deny Access by Default](mitigation-library.md#deny-access-by-default) (Preventive)
- [Disable HTTP redirections and implement a robust URL parser for client input validation.](mitigation-library.md#disable-http-redirections-and-implement-a-robust-url-parser-for-client-input-validation) (Preventive)
- [Implement network segmentation](mitigation-library.md#implement-network-segmentation) (Preventive)
- [Implement URL Validation with Allowlists](mitigation-library.md#implement-url-validation-with-allowlists) (Preventive)
- [Isolate resource fetching mechanisms within the network.](mitigation-library.md#isolate-resource-fetching-mechanisms-within-the-network) (Preventive)
- [Sanitize Output](mitigation-library.md#sanitize-output) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Supply Chain Attacks - Cross-Layer

**Priority:** High · **Likelihood:** Low · **Severity:** Critical · **Framework:** OWASP LLM05

**Affects:** LLM Automation (Agents)

Compromising a component in one layer (e.g., a library in Layer 3) to affect other layers (e.g., the Agent Ecosystem).

**Attacker goal / impact:** A compromise in a lower layer (e.g., OS library) affects higher-level Agent logic.

**Mitigations**

- [Conduct Software Composition Analysis](mitigation-library.md#conduct-software-composition-analysis) (Detective)
- [Conduct targeted security testing for domain-specific risks](mitigation-library.md#conduct-targeted-security-testing-for-domain-specific-risks) (Detective)
- [Enforce code integrity and supply chain security for AI agents](mitigation-library.md#enforce-code-integrity-and-supply-chain-security-for-ai-agents) (Preventive)
- [Enforce SBOM for AI supply chain security](mitigation-library.md#enforce-sbom-for-ai-supply-chain-security) (Preventive)
- [Implement secondary review for uploaded artifacts](mitigation-library.md#implement-secondary-review-for-uploaded-artifacts) (Detective)
- [Perform domain-specific threat modeling for AI agents](mitigation-library.md#perform-domain-specific-threat-modeling-for-ai-agents) (Preventive)
- [Secure Infrastructure-as-Code for AI agent provisioning](mitigation-library.md#secure-infrastructure-as-code-for-ai-agent-provisioning) (Preventive)
- [Utilize trusted repositories for libraries and dependencies](mitigation-library.md#utilize-trusted-repositories-for-libraries-and-dependencies) (Preventive)

### Compromised Observability Tools

**Priority:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents)

Attackers injecting malicious code into monitoring systems that exfiltrate system data or hide malicious behaviour, compromising the integrity and security of the AI monitoring process.

**Attacker goal / impact:** Inject code into monitoring tools to hide malicious behavior or exfiltrate logs.

**Mitigations**

- [Implement a Security Information and Event Management (SIEM) solution.](mitigation-library.md#implement-a-security-information-and-event-management-siem-solution) (Detective)
- [Protect the integrity of observability tools monitoring AI agents](mitigation-library.md#protect-the-integrity-of-observability-tools-monitoring-ai-agents) (Preventive)

### Framework Evasion

**Priority:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents)

AI agents specifically designed to bypass security controls within the framework, using advanced techniques to perform unauthorized actions.

**Attacker goal / impact:** Agents designed specifically to bypass the security controls of the AI framework.

**Mitigations**

- [Apply access and privilege management for AI agents](mitigation-library.md#apply-access-and-privilege-management-for-ai-agents) (Preventive)
- [Establish agent identity and trust verification](mitigation-library.md#establish-agent-identity-and-trust-verification) (Preventive)
- [Establish governance and auditability for AI agents](mitigation-library.md#establish-governance-and-auditability-for-ai-agents) (Detective)
- [Implement behavioral monitoring and anomaly detection for AI agents](mitigation-library.md#implement-behavioral-monitoring-and-anomaly-detection-for-ai-agents) (Detective)
- [Secure security agent control plane and runtime attestation](mitigation-library.md#secure-security-agent-control-plane-and-runtime-attestation) (Preventive)
- [Strengthen robustness of AI security agents against evasion attacks](mitigation-library.md#strengthen-robustness-of-ai-security-agents-against-evasion-attacks) (Preventive)

### Lateral Movement - Cross-Layer

**Priority:** Medium · **Likelihood:** Low · **Severity:** High · **Framework:** STRIDE (Elevation)

**Affects:** LLM Automation (Agents)

An attacker gaining access to one layer (e.g., Layer 4) and then using that access to compromise other layers (e.g., Data Infrastructure).

**Attacker goal / impact:** Move from one logical layer (e.g., Application) to another (e.g., Data).

**Mitigations**

- [Deny Access by Default](mitigation-library.md#deny-access-by-default) (Preventive)
- [Detect and prevent lateral movement in AI infrastructure](mitigation-library.md#detect-and-prevent-lateral-movement-in-ai-infrastructure) (Preventive)
- [Harden and monitor orchestration platforms for AI agents](mitigation-library.md#harden-and-monitor-orchestration-platforms-for-ai-agents) (Preventive)
- [Implement Downstream Authorization Checks](mitigation-library.md#implement-downstream-authorization-checks) (Preventive)
- [Implement extreme least privilege access controls](mitigation-library.md#implement-extreme-least-privilege-access-controls) (Preventive)
- [Implement human approval for high-impact actions](mitigation-library.md#implement-human-approval-for-high-impact-actions) (Preventive)
- [Implement Just-In-Time and Just-Enough-Access controls](mitigation-library.md#implement-just-in-time-and-just-enough-access-controls) (Preventive)
- [Implement user tracking for minimum permission enforcement](mitigation-library.md#implement-user-tracking-for-minimum-permission-enforcement) (Detective)
- [Update configurations regularly](mitigation-library.md#update-configurations-regularly) (Preventive)

### Poisoning Observability Data

**Priority:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents)

Manipulating the data fed into the observability system for AI systems, hiding incidents from security teams and masking malicious activity.

**Attacker goal / impact:** Feed false data to monitoring systems to mask attacks or trigger false alarms.

**Mitigations**

- [Implement behavioral monitoring and anomaly detection for AI agents](mitigation-library.md#implement-behavioral-monitoring-and-anomaly-detection-for-ai-agents) (Detective)
- [Protect the integrity of observability tools monitoring AI agents](mitigation-library.md#protect-the-integrity-of-observability-tools-monitoring-ai-agents) (Preventive)

### Resource Hijacking

**Priority:** Medium · **Likelihood:** Medium · **Severity:** Medium · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents)

Attackers using compromised AI infrastructure for cryptomining or other illicit purposes, leading to performance degradation of AI agents.

**Attacker goal / impact:** Use the AI infrastructure for unauthorized tasks like cryptomining.

**Mitigations**

- [Implement API rate limiting](mitigation-library.md#implement-api-rate-limiting) (Preventive)
- [Implement resource limits](mitigation-library.md#implement-resource-limits) (Preventive)
- [Isolate resource fetching mechanisms within the network.](mitigation-library.md#isolate-resource-fetching-mechanisms-within-the-network) (Preventive)
- [Limit resource usage per request.](mitigation-library.md#limit-resource-usage-per-request) (Preventive)
- [Monitor LLM resource utilization for anomalies](mitigation-library.md#monitor-llm-resource-utilization-for-anomalies) (Detective)

## API Security & Access Control Threats

### Broken Authentication

**Priority:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** OWASP API02

**Affects:** Server-side functions, Application Services

Attackers could target authentication mechanisms, potentially gaining complete control of other users' accounts, accessing their data, and performing actions on their behalf.

**Attacker goal / impact:** Hijack user/agent accounts to access data or perform actions on their behalf.

**Mitigations**

- [Deploy anti-brute force protections](mitigation-library.md#deploy-anti-brute-force-protections) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Map all authentication flows](mitigation-library.md#map-all-authentication-flows) (Preventive)
- [Secure credential recovery endpoints](mitigation-library.md#secure-credential-recovery-endpoints) (Preventive)

### Broken Object Level Authorization

**Priority:** Critical · **Likelihood:** High · **Severity:** Critical · **Framework:** OWASP API01

**Affects:** Server-side functions, Application Services

An attacker could exploit API endpoints with broken object-level authorization by manipulating the object ID in the request, leading to unauthorized access to data.

**Attacker goal / impact:** Manipulate IDs to access data belonging to other users (BOLA).

**Mitigations**

- [Implement access control mechanisms](mitigation-library.md#implement-access-control-mechanisms) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)
- [Implement random and unpredictable record IDs](mitigation-library.md#implement-random-and-unpredictable-record-ids) (Preventive)
- [Implement record-level authorization checks for all API endpoints](mitigation-library.md#implement-record-level-authorization-checks-for-all-api-endpoints) (Preventive)

### Privilege Escalation

**Priority:** Critical · **Likelihood:** Medium · **Severity:** Critical · **Framework:** STRIDE (Elevation)

**Affects:** LLM Automation (Agents)

An agent or attacker gaining unauthorized privileges in one layer, and using it to access or manipulate others.

**Attacker goal / impact:** Gain unauthorized privileges in one layer to manipulate others.

**Mitigations**

- [Implement access control mechanisms](mitigation-library.md#implement-access-control-mechanisms) (Preventive)
- [Implement extreme least privilege access controls](mitigation-library.md#implement-extreme-least-privilege-access-controls) (Preventive)
- [Implement Just-In-Time and Just-Enough-Access controls](mitigation-library.md#implement-just-in-time-and-just-enough-access-controls) (Preventive)
- [Secure Service Token Management](mitigation-library.md#secure-service-token-management) (Preventive)

### Broken Function Level Authorization

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP API05

**Affects:** Server-side functions, Application Services

An attacker could send legitimate API calls to endpoints they should not have access to, leading to unauthorized access to functionality and potentially service disruption.

**Attacker goal / impact:** Standard users accessing admin-only API endpoints.

**Mitigations**

- [Implement access control mechanisms](mitigation-library.md#implement-access-control-mechanisms) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)

### Bypass Access Control

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP API05

**Affects:** Server-side functions, Application Services

As an attacker, I aim to bypass access control checks by modifying the URL via parameter tampering or force browsing, altering the internal application state, manipulating the HTML page, or using specialized attack tools to modify API requests.

**Attacker goal / impact:** Circumvent checks via URL tampering or forced browsing.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Improper Inventory Management

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** OWASP API09

**Affects:** Server-side functions, Application Services

Attackers could gain unauthorized access through old API versions, unpatched endpoints, or third parties with weaker security, leading to data leaks or server takeover.

**Attacker goal / impact:** Attack old/unpatched API versions ("Zombie APIs") to gain access.

**Mitigations**

- [Automate API documentation generation and restrict access to authorized users only](mitigation-library.md#automate-api-documentation-generation-and-restrict-access-to-authorized-users-only) (Preventive)
- [Catalog integrated services and their data handling](mitigation-library.md#catalog-integrated-services-and-their-data-handling) (Detective)
- [Document API endpoints](mitigation-library.md#document-api-endpoints) (Detective)

### Missing authentication

**Priority:** High · **Likelihood:** Low · **Severity:** High · **Framework:** OWASP API02

**Affects:** Server-side functions, Application Services

The product does not perform any authentication for functionality that requires a provable user identity or consumes a significant amount of resources.

**Attacker goal / impact:** Access critical functions without any identity verification.

**Mitigations**

- [Implement centralized authentication](mitigation-library.md#implement-centralized-authentication) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Security Misconfiguration (API)

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** OWASP API08

**Affects:** Server-side functions, Application Services

Attackers might exploit unpatched flaws, services with insecure default configurations, or unprotected files and directories, potentially leading to unauthorized access or system compromise.

**Attacker goal / impact:** Exploit default settings or unprotected files to compromise the system.

**Mitigations**

- [Automate configuration assessments](mitigation-library.md#automate-configuration-assessments) (Detective)
- [Harden Assets Against Attacks](mitigation-library.md#harden-assets-against-attacks) (Preventive)
- [Update configurations regularly](mitigation-library.md#update-configurations-regularly) (Preventive)

### Spoofing

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** STRIDE (Spoofing)

**Affects:** Server-side functions, Application Services

Spoofing is where an attacker masquerades as a trusted entity to gain unauthorized access or deceive recipients.

**Attacker goal / impact:** Masquerade as a trusted entity to deceive recipients or gain access.

**Mitigations**

- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)
- [Implement strong authentication with 2FA or MFA.](mitigation-library.md#implement-strong-authentication-with-2fa-or-mfa) (Preventive)
- [Use Trusted Frameworks](mitigation-library.md#use-trusted-frameworks) (Preventive)

### Unrestricted Resource Consumption

**Priority:** High · **Likelihood:** High · **Severity:** Medium · **Framework:** OWASP API04

**Affects:** LLM Model, Server-side functions, Application Services

Attackers could exploit unrestricted resource consumption, leading to DoS due to resource starvation or increased operational costs.

**Attacker goal / impact:** Exhaust system resources via excessive API calls (DoS).

**Mitigations**

- [Implement API rate limiting](mitigation-library.md#implement-api-rate-limiting) (Preventive)
- [Implement resource limits](mitigation-library.md#implement-resource-limits) (Preventive)
- [Limit parameter and payload sizes](mitigation-library.md#limit-parameter-and-payload-sizes) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Unsafe Consumption of APIs

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** OWASP API10

**Affects:** Server-side functions, Application Services

Attackers might identify and compromise other APIs/services integrated with the target API, leading to sensitive information exposure, injections, or denial of service.

**Attacker goal / impact:** Compromise the system via vulnerabilities in third-party APIs it integrates with.

**Mitigations**

- [Encrypt all data in transit using secure protocols.](mitigation-library.md#encrypt-all-data-in-transit-using-secure-protocols) (Preventive)
- [Evaluate service provider API security](mitigation-library.md#evaluate-service-provider-api-security) (Detective)
- [Validate and sanitize API inputs](mitigation-library.md#validate-and-sanitize-api-inputs) (Preventive)

## Denial of Service (DoS) Threats

### Denial of Service via Query Flooding

**Priority:** High · **Likelihood:** Medium · **Severity:** High · **Framework:** STRIDE (DoS)

**Affects:** Vector DB

Flooding the vector search API with high-dimensional queries to exhaust compute.

**Attacker goal / impact:** Flood the Vector DB with high-dimensional queries to crash the search index.

**Mitigations**

- [Rate Limiting, Quotas, and Cost-Aware Throttling](mitigation-library.md#rate-limiting-quotas-and-cost-aware-throttling) (Preventive)
- [Tiered Capacity and DoS-Aware Admission Control](mitigation-library.md#tiered-capacity-and-dos-aware-admission-control) (Preventive)

### LLM Denial of Service

**Priority:** Medium · **Likelihood:** High · **Severity:** Medium · **Framework:** OWASP LLM04

**Affects:** Application Services

An attacker submits queries that lead to recurring resource usage through high-volume generation of tasks in a queue.

**Attacker goal / impact:** Flood the generation queue to degrade service for legitimate users.

**Mitigations**

- [Implement API rate limiting](mitigation-library.md#implement-api-rate-limiting) (Preventive)
- [Limit resource usage per request.](mitigation-library.md#limit-resource-usage-per-request) (Preventive)
- [Validate User Input](mitigation-library.md#validate-user-input) (Preventive)

### Manipulation of Evaluation Metrics

**Priority:** Medium · **Likelihood:** Low · **Severity:** Medium · **Framework:** STRIDE (Tampering)

**Affects:** LLM Automation (Agents), Fine-tuning data, Training data

Adversaries influencing benchmarks to favor their AI agents, through poisoned datasets or biased test cases, resulting in inaccurate performance data.

**Attacker goal / impact:** Poison benchmarks to make a malicious agent appear effective/safe.

**Mitigations**

- [Protect evaluation pipelines for AI agents from manipulation](mitigation-library.md#protect-evaluation-pipelines-for-ai-agents-from-manipulation) (Preventive)

## Additional threats

### Broken Object Property Level Authorization

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** Server-side functions, Application Services

An attacker could access private/sensitive object properties, potentially leading to data disclosure, corruption, or unauthorized privilege escalation.

**Mitigations**

- [Implement property-level access controls](mitigation-library.md#implement-property-level-access-controls) (Preventive)
- [Implement schema-based response validation](mitigation-library.md#implement-schema-based-response-validation) (Preventive)
- [Limit property exposure](mitigation-library.md#limit-property-exposure) (Preventive)

### Cache Poisoning (semantic or vector cache)

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** RAG private data stores

Manipulated cache entries return altered or malicious retrievals.

**Mitigations**

- [Enforce Strict Authenticated Cache Writes with Provenance Validation](mitigation-library.md#enforce-strict-authenticated-cache-writes-with-provenance-validation) (Preventive)
- [Validate and Re-Score Retrieved Cache Entries Against a Trusted Source](mitigation-library.md#validate-and-re-score-retrieved-cache-entries-against-a-trusted-source) (Preventive)

### Denial of Service

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** Server-side functions, Application Services

Denial of service (DoS) is an attack that disrupts the normal functioning of a system or network by overwhelming it with excessive traffic or requests.

**Mitigations**

- [Implement Distributed Architecture](mitigation-library.md#implement-distributed-architecture) (Preventive)

### Denial of Service (DoS) Attacks - AI infrastructure

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** LLM Automation (Agents)

Overwhelming infrastructure resources supporting AI agents, causing the AI systems to become unavailable to legitimate users.

**Mitigations**

- [Implement API rate limiting](mitigation-library.md#implement-api-rate-limiting) (Preventive)
- [Implement Distributed Architecture](mitigation-library.md#implement-distributed-architecture) (Preventive)
- [Implement resource limits](mitigation-library.md#implement-resource-limits) (Preventive)
- [Isolate resource fetching mechanisms within the network.](mitigation-library.md#isolate-resource-fetching-mechanisms-within-the-network) (Preventive)
- [Limit resource usage per request.](mitigation-library.md#limit-resource-usage-per-request) (Preventive)
- [Monitor LLM resource utilization for anomalies](mitigation-library.md#monitor-llm-resource-utilization-for-anomalies) (Detective)

### Denial of Service (DoS) Attacks - AI model

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** LLM Automation (Agents)

Attackers overwhelming foundation models with computationally expensive queries or adversarially crafted inputs (such as sponge attacks that exploit model complexity vulnerabilities) to exhaust computational resources, degrade inference performance, or cause service unavailability at the model level. They can potentially disrupt legitimate users' access to AI capabilities and compromise agentic AI systems' ability to perform autonomous tasks. This results in operational downtime, cascade failures across dependent AI agents, and increased computational costs.

**Mitigations**

- [Defend AI models against sponge and resource-exhaustion inputs](mitigation-library.md#defend-ai-models-against-sponge-and-resource-exhaustion-inputs) (Preventive)
- [Enforce least privilege access for LLMs](mitigation-library.md#enforce-least-privilege-access-for-llms) (Preventive)
- [Limit LLM Plugin Functions](mitigation-library.md#limit-llm-plugin-functions) (Preventive)
- [Monitor LLM resource utilization for anomalies](mitigation-library.md#monitor-llm-resource-utilization-for-anomalies) (Detective)
- [Restrict LLM Plugin Permissions](mitigation-library.md#restrict-llm-plugin-permissions) (Preventive)
- [Restrict plugin access](mitigation-library.md#restrict-plugin-access) (Preventive)

### Denial of Service on Data Infrastructure

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** LLM Automation (Agents)

Disrupting access to data needed by AI agents, preventing agent functionality and interrupting normal operation of the AI systems.

**Mitigations**

- [Ensure resilience of AI data infrastructure against DOS attacks](mitigation-library.md#ensure-resilience-of-ai-data-infrastructure-against-dos-attacks) (Preventive)

### Denial of Service on Evaluation Infrastructure

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** LLM Automation (Agents)

Disrupting the AI evaluation process to prevent proper testing and detection of compromised behavior, leading to a lack of visibility of AI agent performance.

**Mitigations**

- [Ensure availability and resilience of AI agent evaluation infrastructure](mitigation-library.md#ensure-availability-and-resilience-of-ai-agent-evaluation-infrastructure) (Preventive)

### Denial of Service on Framework APIs

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** LLM Automation (Agents)

Disrupting the AI framework’s ability to function, overloading services and preventing normal operation for the AI agents.

**Mitigations**

- [Defend framework APIs against distributed denial-of-service (DDoS) attacks](mitigation-library.md#defend-framework-apis-against-distributed-denial-of-service-ddos-attacks) (Preventive)
- [Implement API rate limiting](mitigation-library.md#implement-api-rate-limiting) (Preventive)

### Elevation of Privilege

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** Server-side functions, Application Services

Elevation of privilege is when an attacker gains unauthorized access to higher-level permissions or rights within a system or application.

**Mitigations**

- [Implement Access Control Measures](mitigation-library.md#implement-access-control-measures) (Preventive)
- [Implement Attribute-Based Access Control (ABAC)](mitigation-library.md#implement-attribute-based-access-control-abac) (Preventive)
- [Implement Role-Based Access Control (RBAC)](mitigation-library.md#implement-role-based-access-control-rbac) (Preventive)

### Embedding Inversion / Reconstruction

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** Vector DB, RAG private data stores

Attackers steal embeddings and use model inversion techniques to approximate original text or images.

**Mitigations**

- [Access-Controlled Embedding Exposure](mitigation-library.md#access-controlled-embedding-exposure) (Preventive)
- [Differential Privacy and Embedding Sanitization](mitigation-library.md#differential-privacy-and-embedding-sanitization) (Preventive)
- [Privacy-Preserving Embedding Generation and Export Policies](mitigation-library.md#privacy-preserving-embedding-generation-and-export-policies) (Preventive)
- [Restricted Embedding Access and Encrypted Storage](mitigation-library.md#restricted-embedding-access-and-encrypted-storage) (Preventive)

### Evasion of Detection

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** LLM Automation (Agents)

AI agents designed to avoid triggering alerts or being flagged by observability systems, using advanced techniques to disguise their true behaviour and avoiding security alerts.

**Mitigations**

- [Conduct targeted security testing for domain-specific risks](mitigation-library.md#conduct-targeted-security-testing-for-domain-specific-risks) (Detective)
- [Implement behavioral monitoring and anomaly detection for AI agents](mitigation-library.md#implement-behavioral-monitoring-and-anomaly-detection-for-ai-agents) (Detective)

### Horizontal/Vertical Solution Vulnerabilities

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** LLM Automation (Agents)

Exploiting weaknesses specific to industry or function-specific AI agent solutions, taking advantage of the unique design of vertical solutions.

**Mitigations**

- [Conduct targeted security testing for domain-specific risks](mitigation-library.md#conduct-targeted-security-testing-for-domain-specific-risks) (Detective)
- [Develop a comprehensive threat model](mitigation-library.md#develop-a-comprehensive-threat-model) (Preventive)
- [Map industry regulations to AI agent design](mitigation-library.md#map-industry-regulations-to-ai-agent-design) (Preventive)
- [Perform domain-specific threat modeling for AI agents](mitigation-library.md#perform-domain-specific-threat-modeling-for-ai-agents) (Preventive)

### Infrastructure-as-Code (IaC) Manipulation

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** LLM Automation (Agents)

Tampering with Terraform or CloudFormation scripts to provision compromised AI resources, leading to the creation of insecure deployment infrastructure for AI agents.

**Mitigations**

- [Secure Infrastructure-as-Code for AI agent provisioning](mitigation-library.md#secure-infrastructure-as-code-for-ai-agent-provisioning) (Preventive)

### Inject malicious stuff into training process

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** LLM Model, Fine-tuning data, Training data

A malicious actor can directly inject falsified, biased, or harmful content into the training processes of a model, which is returned in subsequent outputs.

**Mitigations**

- [Architect distinct LLMs for specific use cases.](mitigation-library.md#architect-distinct-llms-for-specific-use-cases) (Preventive)
- [Implement Data Version Control](mitigation-library.md#implement-data-version-control) (Corrective)
- [Implement robust sandboxing measures](mitigation-library.md#implement-robust-sandboxing-measures) (Preventive)
- [Implement User-Supplied Info in Vector Database](mitigation-library.md#implement-user-supplied-info-in-vector-database) (Preventive)
- [Verify data source legitimacy](mitigation-library.md#verify-data-source-legitimacy) (Preventive)

### Tampering

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** Server-side functions, Application Services

Tampering with data involves unauthorized changes to digital information, often with harmful intent, making it unreliable and leading to serious consequences.

**Mitigations**

- [Encrypt all sensitive data in transit and at rest](mitigation-library.md#encrypt-all-sensitive-data-in-transit-and-at-rest) (Preventive)
- [Implement hashing for data integrity verification.](mitigation-library.md#implement-hashing-for-data-integrity-verification) (Detective)

### Unauthorized Data Access (Tenant Isolation Failure)

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** Vector DB

Weak namespace or API design allows one tenant to query another’s embeddings or metadata.

**Mitigations**

- [Strong Tenant-Aware Authentication and Index Isolation](mitigation-library.md#strong-tenant-aware-authentication-and-index-isolation) (Preventive)
- [Tenant-Scoped Query Enforcement and Access Policy Checks](mitigation-library.md#tenant-scoped-query-enforcement-and-access-policy-checks) (Preventive)

### Unrestricted Access to Sensitive Business Flows

**Priority:** Unrated · **Likelihood:** n/a · **Severity:** n/a

**Affects:** Server-side functions, Application Services

Attackers could exploit sensitive business flows in APIs, causing harm such as preventing legitimate users from purchasing a product or leading to inflation in a game's internal economy.

**Mitigations**

- [Block Non-Human Traffic](mitigation-library.md#block-non-human-traffic) (Preventive)
- [Implement CAPTCHA for User Verification](mitigation-library.md#implement-captcha-for-user-verification) (Preventive)
- [Implement device fingerprinting to block unauthorized client devices](mitigation-library.md#implement-device-fingerprinting-to-block-unauthorized-client-devices) (Preventive)
