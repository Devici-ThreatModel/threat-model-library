# Web Application: Components and Data Flow

Each element of the reference architecture, with its role and the attributes that drive threat generation. Back to the [model overview](README.md).

| Component | Description | Linked attributes |
|---|---|---|
| User | The human actor interacting with the system. They are the primary initiator of data flows. |  |
| Browser | The client-side application (likely a Single Page Application or SPA) running on the user's device. It handles the UI presentation and communicates with the CDN and API Gateway. | Browser |
| Authentication App | An external device or application (e.g., Google Authenticator, Authy) used to generate Time-based One-Time Passwords (TOTP) for Multi-Factor Authentication (MFA). | Mobile App |
| SMS / Text Code | An out-of-band communication channel used to deliver One-Time Passwords (OTP) to the user's mobile device for MFA. | text message, Authentication Code |
| Gateway Layer | Trust Boundry |  |
| API Gateway | The single entry point for all dynamic API traffic. It routes incoming requests from the Browser to the appropriate backend service (Data Plane) and likely handles initial request termination (TLS) | API, Multi-factor authentication, API Gateway |
| Data Plane Layer (Application Services) | Trust Boundry |  |
| Content / Domain Data Service | The microservice responsible for the core business logic and CRUD operations related to the application's primary content. | Express.js (Node.js), Microservice |
| User Profile / Account Service | The microservice responsible for managing user-specific data, such as profile settings, preferences, and account details. | Express.js (Node.js), Microservice |
| Authentication & Authorization Service | The internal security authority. It validates credentials and permissions for the other services to ensure only authorized requests are processed. | Express.js (Node.js), Microservice |
| Database Layer (Persistence) | Trust Boundry |  |
| content_db (Postgres) | The dedicated relational database storing business data for the Content Service. | Postgres |
| user_db (Postgres) | The dedicated relational database storing profile information for the User Profile Service. | Postgres |
| auth_db (Postgres) | The dedicated relational database storing internal authorization rules, roles, and potentially session states for the Auth Service. | Postgres |
| Cloud Layer (Infrastructure & Support) | Trust Boundry |  |
| Content Delivery Network (CDN) | A distributed network of servers that caches and delivers static assets (images, JavaScript, CSS) to the Browser to improve performance and reduce latency. | Content Delivery Network |
| Identity Provider (IdP) | A centralized service (likely a third-party managed service like Auth0, AWS Cognito, or Azure AD) that handles the core identity verification and MFA enforcement. | Identity Management |
| User Database (Cloud) | The backing directory or user store specifically used by the Identity Provider to manage credentials and identity attributes (distinct from the application's internal user_db). | Database |
| Log Collector | A centralized component that aggregates logs and telemetry data from the API Gateway and Application Services for monitoring. | SIEM |
| Log Database | The storage repository where aggregated logs are persisted for auditing, debugging, and security analysis. | log, Database |
