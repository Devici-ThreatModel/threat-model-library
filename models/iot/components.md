# IoT Device: Components and Data Flow

Each element of the reference architecture, with its role and the attributes that drive threat generation. Back to the [model overview](README.md).

| Component | Description | Linked attributes |
|---|---|---|
| Air Quality & Comfort Device | The physical trust boundary representing the local smart device hardware installed in the home. |  |
| MEMS Sensors | (Micro-Electro-Mechanical Systems) Hardware sensors collecting real-time temperature, humidity, and air quality data. | MEMS Sensor |
| Local Data Aggregator | Internal software component that collects and normalizes raw readings from the sensors before storage. |  |
| Local Data Store | Temporary on-device storage (cache/buffer) ensuring data availability for local commands or when offline. | Database |
| Data Transporter | The communication module responsible for securely uploading telemetry to the cloud and receiving updates. |  |
| Command Module | The decision logic engine that translates user inputs or cloud insights into physical control signals. | API |
| Cloud Layer | The trust boundary representing the remote server infrastructure (likely AWS based on component names). |  |
| Universal Data Aggregator | The cloud ingress point (likely an IoT Broker) that ingests high-volume telemetry from many devices. | API |
| Amazon S3 | Scalable cloud object storage used to persist historical sensor data and system logs. | AWS S3 |
| Amazon SageMaker | Machine learning service that analyzes historical data to generate predictive comfort models and efficiency insights. | Analytics and Usage Statistics |
| Integration APIs | The interface layer allowing external apps, voice assistants, and the device itself to exchange data and commands. | API |

## External Systems & User Interfaces

| Component | Description | Linked attributes |
|---|---|---|
| Voice Assistants | Third-party external platforms (e.g., Alexa, Google Assistant) allowing voice control of the system. | amazon alexa |
| Mobile/Web App | The remote user interface allowing the human user to monitor and control the system via smartphone or browser. |  |
| Human User | The end-user interacting with the system via touch, voice, or mobile apps. |  |
| HVAC System | (Heating, Ventilation, and Air Conditioning) The physical external system controlled by the device to regulate temperature. |  |
| Air Purifier | The physical external appliance controlled by the device to filter air particulates. |  |
| Thermostat Touch Display | The local physical interface allowing the user to view status and manually adjust settings. |  |
