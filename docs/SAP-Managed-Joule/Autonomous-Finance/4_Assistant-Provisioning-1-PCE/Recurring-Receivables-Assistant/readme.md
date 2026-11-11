# Recurring Receivables Assistant — PCE Provisioning

This directory contains the provisioning documentation for the **Recurring Receivables Assistant** on **SAP S/4HANA Cloud Private Edition**.

> **Note:** This assistant is currently part of an SAP Early Adopter Care (EAC) program. Contact your SAP Account Executive for access.

## About this Assistant

The Recurring Receivables Assistant helps manage subscription contracts, convergent invoicing, and contract accounting collections. It targets businesses that operate recurring billing models and require automated management of subscription lifecycle, invoicing execution, and collections insights for contract accounting (FI-CA) customers.

## Agents in this Assistant

| Agent | Purpose |
|-------|---------|
| Subscription Lifecycle Agent | Manages subscription contract changes such as extensions, cancellations, and PO reference updates |
| Convergent Invoice Execution Agent | Handles convergent invoicing document management and billing execution |
| Collection Insights Agent | Provides collection insights and dunning analysis for contract accounting (FI-CA) customers |

## Mission Structure

| File | Content |
|------|---------|
| [4.1 — Provisioning in SAP for Me](./4.1_Provisioning_in_SAP4Me.md) | Step-by-step activation wizard in SAP for Me |
| [4.2 — Post-Provisioning Validations](./4.2_Post-Provisioning_Validations.md) | BTP resources, formation, and CIS groups validation |
| [4.3 — Subscription Lifecycle Agent](./4.3_Subscription_Lifecycle_Agent.md) | Objective, capabilities, and example prompts |
| [4.4 — Convergent Invoice Execution Agent](./4.4_Convergent_Invoice_Execution_Agent.md) | Objective, capabilities, and example prompts |
| [4.5 — Collection Insights Agent](./4.5_Collection_Insights_Agent.md) | Objective, capabilities, and example prompts |
| [4.6 — CIS Authorizations / AMS Policies](./4.6_CIS_Authorizations_AMS_Policies.md) | User group assignment in SAP Cloud Identity Services |
| [4.7 — Test Scripts](./4.7_Test_Scripts.md) | Validation scenarios after provisioning |
| [4.8 — Support Contact](./4.8_Support_Contact.md) | Support channels and useful resources |

## How to Navigate

1. Complete the system-level prerequisites in [2_Prepare](../../2_Prepare/).
2. Follow [4.1](./4.1_Provisioning_in_SAP4Me.md) to activate the assistant in SAP for Me.
3. Run [4.2](./4.2_Post-Provisioning_Validations.md) to verify BTP and CIS configuration.
4. Review the individual agent files to understand what each agent can do and test with the provided example prompts.
5. Assign users via [4.6](./4.6_CIS_Authorizations_AMS_Policies.md).
