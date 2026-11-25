# Automotive: Components and Data Flow

Each element of the reference architecture, with its role and the attributes that drive threat generation. Back to the [model overview](README.md).

## Infotainment & User Interface

| Component | Description | Linked attributes |
|---|---|---|
| Infotainment System | Trust Boundary: The user-facing hub responsible for entertainment, information, and managing user inputs. |  |
| Touch Screen Controller | The hardware interface that processes input from the touch screen and relays it to the system. | touch screen controller |
| Touch Screen | The primary visual display and input interface for the driver and passengers. |  |
| Rear Screen(s) | Display units providing entertainment specifically for rear passengers. |  |
| Microphone | Captures audio for voice commands, hands-free calling, and cabin monitoring. | microphone |
| Cameras | Visual sensors providing video feeds for parking assistance, reversing, or safety features. | camera |
| Bluetooth Controller | The internal module managing wireless Bluetooth communication logic and pairing. | Bluetooth Beacon |
| Bluetooth | Wireless protocol connecting external mobile devices to the vehicle for audio/data. |  |
| USB Controller | The hardware interface managing data transfer and power for USB connections. | USB |
| USB Ports | Physical interfaces allowing users to plug in flash drives, phones, or charging cables. |  |
| HVAC Controller | Digital controller within the infotainment system managing heating, ventilation, and A/C. |  |
| Cabin Temperature Sensor | Measures the interior ambient temperature to help regulate climate control. |  |

## Computing System

| Component | Description | Linked attributes |
|---|---|---|
| Computing System | Trust Boundary: The central architectural block bridging user inputs (Infotainment) with vehicle functions (CAN Bus). |  |
| Onboard Computer | The main CPU/GPU processing unit that executes vehicle logic and routes data. |  |
| Infotainment OS | The operating system (e.g., Android Automotive, QNX) running on the computing hardware. | Android |
| Hardware Security Module (HSM) | Tamper-resistant crypto chip that stores private keys and verifies signatures for secure boot, OTA update verification and message authentication. |  |

## CAN Bus & Vehicle Control (ECUs)

| Component | Description | Linked attributes |
|---|---|---|
| CAN Bus | Trust Boundary: The internal network allowing ECUs to communicate without a central host computer. |  |
| Central Gateway ECU | Dedicated gateway between the computing system and the CAN network. Separates network domains, filters and authenticates cross-domain messages, and enforces diagnostic access policy. All ECU traffic to the onboard computer passes through it. |  |
| Engine & Powertrain ECU | Computer controlling engine performance, fuel injection, and power delivery. |  |
| Engine & Powertrain | The physical mechanical assembly (motor, drivetrain) managed by the ECU. |  |
| Transmission ECU | Computer controlling gear shifting and transmission behavior. |  |
| Transmission | The physical gearbox system transferring power to the wheels. |  |
| Braking & Safety ECU | Critical computer managing deceleration and passenger safety systems. |  |
| ABS, Traction Control, Airbags | Physical safety mechanisms actuated by the Braking & Safety ECU. |  |
| Body & Comfort Systems ECU | Computer managing non-critical body functions like windows and seats. |  |
| Windows, Mirrors, Seats, Lighting & HVAC | Physical components controlling passenger comfort and visibility. |  |
| Keyless Entry Receiver | Radio receiver (RKE/PKE) that listens for the key fob on its own frequency and passes lock, unlock and start requests to the Body & Comfort Systems ECU. |  |
| Advanced Driver Assistance ECU | Computer processing data for semi-autonomous features (ADAS). |  |
| Lane Keeping, Cruise Control, Parking Sensors | Sensors and actuators enabling driver assistance features. |  |

## Network & External Actors

| Component | Description | Linked attributes |
|---|---|---|
| Network | Trust Boundary: The boundary containing the vehicle's external wireless communication modules. |  |
| Wifi | Wireless module connecting the vehicle to the internet or local networks (e.g., for updates). | Wifi |
| GPS | Receiver module calculating vehicle location based on satellite signals. | GPS |
| GPS Satellites | External orbital infrastructure sending timing and positioning data. |  |
| Vehicle Manufacturer | External OEM cloud infrastructure for software updates and telemetry. |  |
| Internet Data Sources | Third-party external servers providing traffic data, media, or weather. |  |
| Human | The driver or passenger initiating inputs and consuming system outputs. |  |
| Mobile Phone or Tablet | Personal external devices connected to the vehicle via Bluetooth or USB. |  |

## Physical Access & Diagnostics

| Component | Description | Linked attributes |
|---|---|---|
| OBD-II Port | Physical diagnostic port, usually under the steering wheel, giving wired access to the vehicle network through the central gateway. |  |
| Diagnostic Tool or Aftermarket Dongle | Workshop scan tool, key programmer, or insurance/telematics dongle plugged into the OBD-II port. |  |
| Key Fob | The owner's radio key fob, separate from Bluetooth and Wi-Fi. |  |
