# IoT Device Reference Threat Model

A smart air-quality system: sensors, an on-device data aggregator and store, a data transporter, cloud analytics, HVAC and air-quality control, and third-party integration APIs.

**Importable model:** [`iot-device.otm.json`](iot-device.otm.json)

## Scope

**In scope:** The device, its cloud backend, and integration APIs.

**Out of scope:** Physical installation and HVAC hardware internals.

## Assumptions

Devices are deployed in user-controlled, physically accessible environments.

## Known gaps

An IoT gateway / device shadow is not modeled; add it if your architecture uses one.

See [Importing into Devici](../../docs/importing-into-devici.md) to load this model.
