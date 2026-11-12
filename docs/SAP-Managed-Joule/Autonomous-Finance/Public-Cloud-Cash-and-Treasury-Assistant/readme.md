# Cash and Treasury Assistant — Public Cloud Provisioning

This directory contains the provisioning documentation for the **Cash and Treasury Assistant** on **SAP S/4HANA Cloud Public Edition**.

## About this Assistant

The Cash and Treasury Assistant helps treasury teams manage cash positioning and bank relationship activities. It uses an orchestration agent that dispatches requests to specialised sub-agents, enabling treasury professionals to monitor liquidity, manage bank accounts, and take informed cash management actions directly through Joule.

## Agents in this Assistant

| Agent | Purpose |
|-------|---------|
| Cash and Treasury Orchestration Agent | Routes requests to the appropriate treasury sub-agents |
| Cash Positioning Agent | Provides visibility into cash positions across bank accounts and supports daily liquidity management |
| Bank Relationship Agent | Manages bank account master data and supports bank relationship activities |

## Mission Structure

| File | Content |
|------|---------|
| [3.1 — Provisioning in SAP for Me](./3.1_Provisioning_in_SAP4Me.md) | Step-by-step activation wizard in SAP for Me |
| [3.2 — Post-Provisioning Validations](./3.2_Post-Provisioning_Validations.md) | BTP resources, formation, and CIS groups validation |
| [3.3 — Cash Positioning Agent](./3.3_Cash_Positioning_Agent.md) | Objective, capabilities, and example prompts |
| [3.4 — Bank Relationship Agent](./3.4_Bank_Relationship_Agent.md) | Objective, capabilities, and example prompts |
| [3.5 — Cash and Treasury Orchestration Agent](./3.5_Cash_and_Treasury_Orchestration_Agent.md) | Objective, sub-agents coordinated, and example prompts |
| [3.6 — Test Scripts](./3.6_Test_Scripts.md) | Validation scenarios after provisioning |
| [3.7 — Support Contact](./3.7_Support_Contact.md) | Support channels and useful resources |

## How to Navigate

1. Complete the system-level prerequisites in [2_Prepare](../../2_Prepare/).
2. Follow [3.1](./3.1_Provisioning_in_SAP4Me.md) to activate the assistant in SAP for Me.
3. Run [3.2](./3.2_Post-Provisioning_Validations.md) to verify BTP and CIS configuration.
4. Review the individual agent files to understand what each agent can do and test with the provided example prompts.
5. Run validation scenarios from [3.6 — Test Scripts](./3.6_Test_Scripts.md).
