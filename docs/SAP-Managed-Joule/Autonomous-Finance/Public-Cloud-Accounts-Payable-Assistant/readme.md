# Accounts Payable Assistant — Public Cloud Provisioning

This directory contains the provisioning documentation for the **Accounts Payable Assistant** on **SAP S/4HANA Cloud Public Edition**.

## About this Assistant

The Accounts Payable Assistant helps AP accountants manage supplier invoice processing and payment clearing operations. It uses an orchestration agent that dispatches requests to specialised sub-agents, enabling AP teams to handle payment inquiries and clearing activities for open payable items directly through Joule.

## Agents in this Assistant

| Agent | Purpose |
|-------|---------|
| Accounts Payable Orchestration Agent | Routes requests to the appropriate AP sub-agents across invoice processing and payment operations |
| Payment Inquiry Handling Agent | Handles payment inquiries, ad-hoc payments, and invoice searches for supplier invoices |
| Receivables and Payables Clearing Agent | Generates clearing proposals for open receivable and payable items |

## Mission Structure

| File | Content |
|------|---------|
| [3.1 — Provisioning in SAP for Me](./3.1_Provisioning_in_SAP4Me.md) | Step-by-step activation wizard in SAP for Me |
| [3.2 — Post-Provisioning Validations](./3.2_Post-Provisioning_Validations.md) | BTP resources, formation, and CIS groups validation |
| [3.3 — Payment Inquiry Handling Agent](./3.3_Payment_Inquiry_Handling_Agent.md) | Objective, capabilities, and example prompts |
| [3.4 — Receivables and Payables Clearing Agent](./3.4_Receivables_and_Payables_Clearing_Agent.md) | Objective, capabilities, and example prompts |
| [3.5 — Test Scripts](./3.5_Test_Scripts.md) | Validation scenarios after provisioning |
| [3.6 — Support Contact](./3.6_Support_Contact.md) | Support channels and useful resources |

## How to Navigate

1. Complete the system-level prerequisites in [2_Prepare](../../2_Prepare/).
2. Follow [3.1](./3.1_Provisioning_in_SAP4Me.md) to activate the assistant in SAP for Me.
3. Run [3.2](./3.2_Post-Provisioning_Validations.md) to verify BTP and CIS configuration.
4. Review the individual agent files to understand what each agent can do and test with the provided example prompts.
5. Run validation scenarios from [3.5 — Test Scripts](./3.5_Test_Scripts.md).
