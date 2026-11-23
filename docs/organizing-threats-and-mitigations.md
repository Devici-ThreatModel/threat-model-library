# Organizing Threats and Mitigations

Our reference models follow a consistent structure for threats and mitigations. Borrow it.

## Group threats by theme

Group threats into themed sections rather than one flat list. Examples:

- Automotive: *Vehicle Control and Safety Critical (CAN Bus and ECUs)*
- IoT: *Cloud and API Security Threats*
- LLM: *LLM-Specific and Prompt Injection Threats*
- Medical: *Patient Safety and Device Integrity*

Themes make it possible to assign ownership (the cloud team owns one group, the firmware team another) and to spot where coverage is thin.

## Describe each threat the same way

| Field | Purpose |
|---|---|
| Threat title | Short and specific |
| Framework category | STRIDE, OWASP, MAESTRO, or similar |
| Description | How the attack works |
| Components affected | Which diagram elements it applies to |
| Attacker goal / impact | What the attacker gains and what it costs you |
| Likelihood | Low, Medium, High |
| Severity | Low, Medium, High, Critical |
| Priority level | Combined result (Low, Medium, High, Critical), used for prioritization |

## Set priority consistently

Likelihood and severity combine into a priority level. In the reference models, severity drives the outcome: a High-likelihood, Critical-severity threat is Critical, and a Low-likelihood, Critical-severity safety threat still lands at High. Pick a rule, write it down, and apply it everywhere. Consistency matters more than the exact matrix.

Work from the top: Critical and High threats first, and confirm each has mitigations before polishing Medium and Low ones.

## Describe each mitigation so someone can act on it

Each mitigation row carries five things beyond its title:

1. **Definition**: what the control is
2. **Considerations**: concrete implementation steps
3. **Explanation**: why it works
4. **Examples**: real products and standards (for example AWS IAM, OAuth 2.0, Open Policy Agent)
5. **Control category**: preventive, detective, or corrective

Tagging the control category exposes imbalance. Most reference models are heavily preventive; if you have almost no detective or corrective controls, you can stop an attack but you won't see or recover from one.

## Keep a curated list and a full model

A full model maps every relevant threat to every component, which is deliberately broad. Alongside it, keep a curated shortlist that you actually score and prioritize. Keep both: broad for coverage, curated for decisions.
