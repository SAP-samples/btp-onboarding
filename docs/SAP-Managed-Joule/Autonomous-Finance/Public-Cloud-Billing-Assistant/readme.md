# Billing Assistant — Public Cloud Provisioning

This directory contains the provisioning documentation for the **Billing Assistant** on **SAP S/4HANA Cloud Public Edition**.

## About this Assistant

The Billing Assistant helps billing clerks and specialists automate billing document processing, detect anomalies, resolve posting errors, and manage billing adjustments. It uses an orchestration agent that dispatches requests to specialised sub-agents covering the full billing lifecycle.

## Agents in this Assistant

| Agent | Purpose |
|-------|---------|
| Billing Orchestration Agent | Coordinates the specialised agents within the Billing Assistant |
| Billing Creation Agent | Prioritizes the billing due list to speed up invoice creation |
| Billing Adjustment Agent | Automates the adjustment of billing documents |
| Billing Anomaly Agent | Detects unusual taxes and abnormal charges and flags anomalies for review |
| Billing Posting Agent | Automates posting-error resolution to keep billing and cash flow on track |
| Error Explanation and Resolution Agent | Detects errors, explains causes, and empowers users to make informed decisions |
| Project Billing Price Verification Agent | Identifies and resolves price discrepancies for project billing specialists |

## Mission Structure

| File | Content |
|------|---------|
| [3.1 — Provisioning in SAP for Me](./3.1_Provisioning_in_SAP4Me.md) | Step-by-step activation wizard in SAP for Me |
| [3.2 — Post-Provisioning Validations](./3.2_Post-Provisioning_Validations.md) | BTP resources, formation, and CIS groups validation |
| [3.3 — Billing Orchestration Agent](./3.3_Billing_Orchestration_Agent.md) | Objective, sub-agents coordinated, and example prompts |
| [3.4 — Billing Creation Agent](./3.4_Billing_Creation_Agent.md) | Objective, capabilities, and example prompts |
| [3.5 — Billing Adjustment Agent](./3.5_Billing_Adjustment_Agent.md) | Objective, capabilities, and example prompts |
| [3.6 — Billing Anomaly Agent](./3.6_Billing_Anomaly_Agent.md) | Objective, capabilities, and example prompts |
| [3.7 — Billing Posting Agent](./3.7_Billing_Posting_Agent.md) | Objective, capabilities, and example prompts |
| [3.8 — Error Explanation and Resolution Agent](./3.8_Error_Explanation_and_Resolution_Agent.md) | Objective, capabilities, and example prompts |
| [3.9 — Project Billing Price Verification Agent](./3.9_Project_Billing_Price_Verification_Agent.md) | Objective, capabilities, and example prompts |
| [3.10 — Test Scripts](./3.10_Test_Scripts.md) | Validation scenarios after provisioning |
| [3.11 — Support Contact](./3.11_Support_Contact.md) | Support channels and useful resources |

## How to Navigate

1. Complete the system-level prerequisites in [2_Prepare](../../2_Prepare/).
2. Follow [3.1](./3.1_Provisioning_in_SAP4Me.md) to activate the assistant in SAP for Me.
3. Run [3.2](./3.2_Post-Provisioning_Validations.md) to verify BTP and CIS configuration.
4. Review the individual agent files to understand what each agent can do and test with the provided example prompts.
5. Run validation scenarios from [3.10 — Test Scripts](./3.10_Test_Scripts.md).
