# Financial Consolidation Assistant — Public Cloud Provisioning

This directory contains the provisioning documentation for the **Financial Consolidation Assistant** on **SAP S/4HANA Cloud Public Edition**.

## About this Assistant

The Financial Consolidation Assistant helps local accountants automate data submissions to the consolidation system and resolve submission errors. It uses an orchestration agent that dispatches requests to specialised sub-agents covering the consolidation data submission lifecycle.

## Agents in this Assistant

| Agent | Purpose |
|-------|---------|
| Financial Consolidation Orchestration Agent | Coordinates the specialised agents within the Financial Consolidation Assistant |
| Financial Consolidation Data Submission Agent | Automates data submissions and helps resolve submission errors |

## Mission Structure

| File | Content |
|------|---------|
| [3.1 — Provisioning in SAP for Me](./3.1_Provisioning_in_SAP4Me.md) | Step-by-step activation wizard in SAP for Me |
| [3.2 — Post-Provisioning Validations](./3.2_Post-Provisioning_Validations.md) | BTP resources, formation, and CIS groups validation |
| [3.3 — Financial Consolidation Orchestration Agent](./3.3_Financial_Consolidation_Orchestration_Agent.md) | Objective, sub-agents coordinated, and example prompts |
| [3.4 — Financial Consolidation Data Submission Agent](./3.4_Financial_Consolidation_Data_Submission_Agent.md) | Objective, capabilities, and example prompts |
| [3.5 — Test Scripts](./3.5_Test_Scripts.md) | Validation scenarios after provisioning |
| [3.6 — Support Contact](./3.6_Support_Contact.md) | Support channels and useful resources |

## How to Navigate

1. Complete the system-level prerequisites in [2_Prepare](../../2_Prepare/).
2. Follow [3.1](./3.1_Provisioning_in_SAP4Me.md) to activate the assistant in SAP for Me.
3. Run [3.2](./3.2_Post-Provisioning_Validations.md) to verify BTP and CIS configuration.
4. Review the individual agent files to understand what each agent can do and test with the provided example prompts.
5. Run validation scenarios from [3.5 — Test Scripts](./3.5_Test_Scripts.md).
