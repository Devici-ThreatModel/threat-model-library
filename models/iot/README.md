# IoT Device Reference Threat Model

This model shows how a smart air system collects sensor data, analyzes it in the cloud, and controls HVAC and air quality for users.

**Scenario:** Smart Air Quality & Comfort Management System

## In this folder

- [`iot-device.otm.json`](iot-device.otm.json): importable model (OTM 0.2.0). See [Importing into Devici](../../docs/importing-into-devici.md).
- [Components and data flow](components.md): every element, its role, and its attributes
- [Threats](threats.md): curated threats by theme, with likelihood, severity, priority, and recommended mitigations
- [`iot-threats-and-mitigations.csv`](iot-threats-and-mitigations.csv): download with full threat descriptions and mitigation guidance (implementation steps, rationale, examples, control category)
- [`iot-components.csv`](iot-components.csv): download of every component and data flow
- [Review notes](review-notes.md): what the model covers, and where it falls short

## At a glance

|  | Count |
|---|---|
| Curated threats documented here | 41 |
| Distinct mitigations | 82 |
| Threat-to-mitigation mappings | 101 |
| Threats in the full importable model | 113 |

The documentation covers the curated set we scored and prioritized. The importable model also includes every additional threat mapped to its components.

| Priority level | Threats |
|---|---|
| Critical | 10 |
| High | 24 |
| Medium | 6 |
| Low | 1 |

| Control type | Mitigations |
|---|---|
| Preventive | 68 |
| Detective | 8 |
| Corrective | 5 |
| Unspecified | 1 |

## System summary

This model shows how a smart air system collects sensor data, analyzes it in the cloud, and controls HVAC and air quality for users.
The system is a hybrid IoT-Cloud solution designed to optimize indoor climate conditions through real-time sensing and machine learning.
- Device Layer (Local): Consists of MEMS Sensors (temperature, humidity, air quality) that feed a Local Data Aggregator. A Command Module executes immediate control signals to the HVAC Unit and Air Purifier. Users interact via a Thermostat Touch Display.
- Cloud Layer (Remote): A Universal Data Aggregator collects telemetry. Amazon S3 provides persistent storage, while Amazon SageMaker performs predictive analytics to refine comfort algorithms.
- Application Services: Integration APIs bridge the gap, enabling feedback loops from the cloud to the device and supporting external interfaces like Voice Assistants and Mobile/Web Apps.

## Scope

In-Scope: The end-to-end logical data flow from local MEMS sensors to cloud analytics and back to physical actuators (HVAC/Purifier). The trust boundaries between the local environment, the cloud infrastructure, and human interfaces.

Out-of-Scope: Physical wiring schematics of the HVAC systems and the internal hardware design of the MEMS sensors.

## Assumptions

The Data Transporter securely authenticates before uploading data to the cloud.

The system fails safe (maintains basic thermostat functionality) if internet connectivity is lost, relying on the Local Data Flow.

Amazon SageMaker models are protected from external manipulation.
