# Accounts Payable Assistant — PCE Provisioning

This directory contains the provisioning documentation for the **Accounts Payable Assistant** on **SAP S/4HANA Cloud Private Edition**.

## About this Assistant

The Accounts Payable Assistant helps AP accountants manage supplier invoice processing and payment clearing operations. It uses an orchestration agent that dispatches requests to specialised sub-agents, enabling AP teams to handle clearing activities for open payable items directly through Joule.

## Agents in this Assistant

| Agent | Purpose |
|-------|---------|
| Accounts Payable Orchestration Agent | Routes requests to the appropriate AP sub-agents across invoice processing and payment operations |
| Receivables and Payables Clearing Agent | Generates clearing proposals for open receivable and payable items |

## Mission Structure

| File | Content |
|------|---------|
| [4.1 — Provisioning in SAP for Me](./4.1_Provisioning_in_SAP4Me.md) | Step-by-step activation wizard in SAP for Me |
| [4.2 — Post-Provisioning Validations](./4.2_Post-Provisioning_Validations.md) | BTP resources, formation, and CIS groups validation |
| [4.3 — Receivables and Payables Clearing Agent](./4.3_Receivables_and_Payables_Clearing_Agent.md) | Objective, capabilities, and example prompts |
| [4.4 — CIS Authorizations / AMS Policies](./4.4_CIS_Authorizations_AMS_Policies.md) | User group assignment in SAP Cloud Identity Services |
| [4.5 — Test Scripts](./4.5_Test_Scripts.md) | Validation scenarios after provisioning |
| [4.6 — Support Contact](./4.6_Support_Contact.md) | Support channels and useful resources |

## How to Navigate

1. Complete the system-level prerequisites in [2_Prepare](../../2_Prepare/).
2. Follow [4.1](./4.1_Provisioning_in_SAP4Me.md) to activate the assistant in SAP for Me.
3. Run [4.2](./4.2_Post-Provisioning_Validations.md) to verify BTP and CIS configuration.
4. Review the individual agent files to understand what each agent can do and test with the provided example prompts.
5. Assign users via [4.4](./4.4_CIS_Authorizations_AMS_Policies.md).
