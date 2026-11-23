# Automotive: Review Notes

An honest review of this reference model: what it covers well and where it falls short. Use it as a checklist when adapting the model to your own system. Back to the [model overview](README.md).

For modeling real-world attacks (like car theft or safety compromises), we must account for these elements as well that are missing from the model

1. The OBD-II Port (On-Board Diagnostics)

- What it is: A physical port usually located under the steering wheel. It is legally mandated in most vehicles for emissions testing and repair.

- Why it is Critical: It provides direct, wired access to the CAN Bus.

- The Threat: This is the #1 vector for "local" attacks. Thieves use this port to program new keys (key cloning), and insurance dongles plugged in here can be hacked remotely to inject messages onto the bus. In your model, a hacker has to go through the Wi-Fi or Infotainment. In reality, they can just plug a laptop into the car.

- Where it goes in the model: Connected directly to the CAN Bus (or the Gateway).

2. The Secure Gateway (Central Gateway ECU)

- What it is: The model shows a generic "Onboard Computer" connecting the Infotainment to the CAN Bus. In a real architecture, this is a dedicated firewall component called the Secure Gateway.

- Why it is Critical: It physically separates the network domains. Real cars do not have just one CAN Bus; they have several (e.g., High-Speed CAN for brakes, Low-Speed CAN for door locks).

- The Threat: Without a Gateway explicitly modeled, you cannot analyze "segmentation" effectively. The Gateway is the only thing stopping a compromised Bluetooth controller from sending a "Deploy Airbag" signal.

- Where it goes in the model: Between the Infotainment System and the CAN Bus.

3. The Hardware Security Module (HSM) / TPM

- What it is: A specialized crypto-chip (like the Secure Enclave in an iPhone) used to store private keys and verify digital signatures.

- Why it is Critical: The model shows "Vehicle Manufacturer" sending updates. How does the car know the update is genuine?

- The Threat: If you don't model the HSM, you miss the risk of Firmware Modification. If an attacker spoofs the manufacturer's server, the car needs an immutable hardware root of trust to reject the fake update.

- Where it goes in the model: Inside the Computing System or embedded within critical ECUs (like the Engine ECU).

4. Keyless Entry Receiver (RKE / PKE)

- What it is: The radio receiver that listens for your physical key fob (Remote Keyless Entry). Your model includes "Mobile Phone," but most cars still rely on RF fobs.

- Why it is Critical: This is a distinct radio frequency (315/433 MHz) separate from Bluetooth or Wi-Fi.

- The Threat: Relay Attacks. This is the most common way modern cars are stolen. Thieves amplify the signal from the key fob inside your house to trick the car into thinking the key is nearby. This vector is completely invisible in the current model.

- Where it goes in the model: An input feeding into the Body & Comfort Systems ECU.

## Mitigations

Many mitigations are too generic for Automotive threat modeling, but they have good coverage.
