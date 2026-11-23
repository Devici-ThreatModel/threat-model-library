# LLM and Agentic Systems: Components and Data Flow

Each element of the reference architecture, with its role and the attributes that drive threat generation. Back to the [model overview](README.md).

## Actors & Clients

| Component | Description | Linked attributes |
|---|---|---|
| User/Client | The legitimate human or system actor initiating requests to the application. | User |
| Malicious Actor | A threat agent attempting to exploit the system (e.g., via Prompt Injection, Denial of Service, or Data Poisoning). |  |

## Application & Production Layer

| Component | Description | Linked attributes |
|---|---|---|
| Application Services | The centralized gateway or backend service that handles user authentication, request validation, and routing before interacting with the AI components. | LLM Prompt, Validated AI Prompt, API |
| LLM Automation (Agents) | The orchestration layer (e.g., LangChain agents) that structures complex queries, maintains context, and coordinates workflows between the user and the model. | AI Multi Agent System |
| LLM Model | The core Large Language Model (e.g., GPT-4, Llama 3) responsible for processing inputs, generating text, and performing inference tasks. | LLM |

## Execution Layer (Tool Use)

| Component | Description | Linked attributes |
|---|---|---|
| Server-side functions | The environment where the LLM can execute code, call internal APIs, or perform actions (e.g., "Plugins" or "Tools") based on its generated outputs. | API |

## Data & Context Layer (RAG)

| Component | Description | Linked attributes |
|---|---|---|
| RAG private data stores | (Retrieval-Augmented Generation) The repository of proprietary documents or knowledge bases used to ground the model's responses in factual data. | RAG (Retrieval-Augmented Generation |
| Vector DB | A specialized database that stores data as vector embeddings, allowing the system to perform semantic search and retrieve relevant context for the LLM. | Vector Database |

## Training & Fine-Tuning Layer

| Component | Description | Linked attributes |
|---|---|---|
| Training data | The massive datasets used for the initial pre-training of the base model. | training set, Training Data, specialized training set |
| Fine-tuning data | Domain-specific datasets used to adapt the model to specific tasks or organizational knowledge. | Fine Tuning Data, refinement dataset |

## External Sources (Untrusted)

| Component | Description | Linked attributes |
|---|---|---|
| External data sources | Third-party repositories or feeds that supply data for training or updates. |  |
| Untrusted medium (Internet) | The public network environment. It is explicitly labeled "Untrusted" because data retrieved from here (e.g., via web browsing tools) opens a path for indirect prompt injection. |  |
