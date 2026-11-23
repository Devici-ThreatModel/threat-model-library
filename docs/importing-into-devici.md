# Importing into Devici

## 1. Create a free account

Go to <https://app.devici.com/sign-up?utm_source=github&utm_campaign=tm_library> and follow the prompts.

## 2. Get the model file

Download the `.otm.json` file from the model's folder under [`models/`](../models). On GitHub, open the file and use **Download raw file**, or clone the repository.

## 3. Import

In Devici, create a new threat model using the OTM import option and choose the downloaded file. The components, data flows, trust boundaries, threats, and mitigations are created for you.

## 4. Adapt it

- Rename components to match your system
- Remove components and flows that don't apply
- Add what is missing from the model's README under "Known gaps"
- Re-prioritize threats using your own likelihood and severity

## Troubleshooting

- **Import fails:** confirm the file is valid JSON and wasn't altered or truncated when downloaded.
- **Diagram looks crowded:** the models are reference-sized. Collapse or delete branches you don't need.
