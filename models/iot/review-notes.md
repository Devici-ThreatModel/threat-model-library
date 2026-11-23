# IoT Device: Review Notes

An honest review of this reference model: what it covers well and where it falls short. Use it as a checklist when adapting the model to your own system. Back to the [model overview](README.md).

## Critical missing elements in the model

- IoT Gateway / Device Shadow:
    - Gap: In cloud IoT architectures (especially AWS), devices typically sync with a "Device Shadow" (a virtual state document) rather than talking directly to a "Universal Aggregator."
    - Risk: Without a shadow state, if the device goes offline, the Mobile App won't know the current status of the HVAC.
- API Gateway / WAF:
    - Gap: The Integration APIs are shown as a bubble. In reality, this requires an API Gateway and potentially a Web Application Firewall (WAF) to filter malicious traffic from the public internet.
- Hardware Security Module (HSM) / Secure Element:
   - Gap: On the device layer, there should be a distinct component for "Key Storage." If the TLS keys for the Data Transporter are stored in the generic Local Data Store, physical extraction attacks are a high risk.

2. Ambiguous or "Extra" Elements

- Universal Data Aggregator: This is a vague term. In an AWS context, this is likely AWS IoT Core (MQTT Broker) or Amazon Kinesis. Naming specific services helps identify specific configuration threats (e.g., "Open MQTT Topic" vs. "Unencrypted Kinesis Stream").
- Data Transporter: This is likely just the TCP/IP or Wi-Fi Stack within the device firmware. Modeling it as a separate bubble is acceptable for logical flow, but technically, it is part of the firmware's communication library.

## Gaps in detected threats

Below is a detailed report of the 4 Critical Gaps preventing this model from being truly comprehensive, along with recommended additions.

1. The "Ransomware & Lockout" Gap (Operational Risk)

 - The current list includes "Denial of Service" (stopping the system), but it omits Ransomware (holding the system hostage).
 - Missing Threat: Ransomware / Logic Locking.
 - Why it matters: Attackers do not just want to stop the HVAC; they often aim to lock it at extreme temperatures (e.g., 90°F / 32°C) and demand payment to unlock control. This has become a primary business model for attacking building management systems.
 - Missing Threat: Legacy Protocol Exploitation (BACnet/Modbus). If the HVAC unit connects to older building systems, attackers can exploit these unencrypted protocols to bypass modern cloud security entirely.

2. The "AI/ML Specific" Gap (SageMaker Risks)

 - The list identifies "Unvalidated sensor data," which acts as input poisoning. However, it misses threats specific to the Amazon SageMaker infrastructure itself.
  - Missing Threat: ML Model Extraction / Inversion. An attacker queries the API repeatedly to reverse-engineer proprietary comfort algorithms.
  - Missing Threat: Notebook/Training Environment Compromise. If SageMaker Jupyter notebooks are not isolated in a Virtual Private Cloud (VPC), an attacker compromising a developer credential can alter the model code directly, not just the data.

3. The "Installer & Config" Gap (Human Factor)

- The list assumes the device is deployed correctly. In reality, HVAC systems are often installed by third-party contractors rather than IT professionals.
- Missing Threat: Insecure Default Installation. There is a significant risk that an installer leaves the device in "Service Mode" or fails to pair it securely because the process is too complex.
- Missing Threat: Shadow IoT / Ghost Devices. A user may install the device but forget about it; it remains on the network unpatched for years, becoming a lateral entry point for other attacks.

4. The "Environmental" Spoofing Gap

- The list covers "Sensor desync," but misses Environmental Spoofing.
- Missing Threat: Analog Interference (Sensor Blinding). An attacker using heat guns, humidity generators, or chemicals (e.g., hairspray near a VOC sensor) can force the HVAC into maximum overdrive without ever touching a digital interface. This constitutes a physical "battery drain" or "cost inflation" attack.

| Category | Recommended Threat Title | Risk Level |
|---|---|---|
| Operational | Ransomware & Remote Control Lockout | Critical |
| AI / ML | Model Extraction / Algorithm Theft (SageMaker) | High |
| Physical | Analog Sensor Spoofing (Environmental Interference) | Medium |
| Network | Lateral Movement via Legacy Protocols (BACnet/Modbus) | High |
| Lifecycle | Insecure Commissioning / Installer Misconfiguration | High |

## Missing Mitigations

Gap A: AI/ML Model Integrity (Amazon SageMaker)

Gap B: Offline Operational Resilience (Safety)

Gap C: Legacy/analog Attack Vectors
