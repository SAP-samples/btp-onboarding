# Financial Closing Assistant — Public Cloud Provisioning

This directory contains the provisioning documentation for the **Financial Closing Assistant** on **SAP S/4HANA Cloud Public Edition**.

## About this Assistant

The Financial Closing Assistant supports finance teams to manage the period close. It uses an orchestration agent that dispatches requests to specialised sub-agents, covering journal entry processing, accrual preparation, analytical insights, and clearing activities.

## Agents in this Assistant

| Agent | Purpose |
|-------|---------|
| Financial Closing Orchestration Agent | Dispatches requests to the appropriate sub-agents in the context of financial closing |
| Accounting Accruals Agent | Automates preparation of manual accruals and generates accrual proposals from a policy handbook |
| Analytical Business Insights Agent | Evaluates company-level financial status through KPIs and creates summary analyses |
| Journal Entry Agent | Automates and simplifies the creation of journal entries from uploaded spreadsheet data |
| Receivables and Payables Clearing Agent | Automatically generates clearing proposals for open receivable and payable items |

> **Note:** The Asset Accounting Anomaly Detection Agent and Financial Consistency Analysis Agent are available on **Private Cloud only** and are not included in this assistant for Public Edition.

## Mission Structure

| File | Content |
|------|---------|
| [3.1 — Provisioning in SAP for Me](./3.1_Provisioning_in_SAP4Me.md) | Step-by-step activation wizard in SAP for Me |
| [3.2 — Post-Provisioning Validations](./3.2_Post-Provisioning_Validations.md) | BTP resources, formation, and CIS groups validation |
| [3.3 — Accounting Accruals Agent](./3.3_Accounting_Accruals_Agent.md) | Objective, capabilities, and example prompts |
| [3.4 — Analytical Business Insights Agent](./3.4_Analytical_Business_Insights_Agent.md) | Objective, capabilities, and example prompts |
| [3.5 — Journal Entry Agent](./3.5_Journal_Entry_Agent.md) | Objective, capabilities, and example prompts |
| [3.6 — Receivables and Payables Clearing Agent](./3.6_Receivables_and_Payables_Clearing_Agent.md) | Objective, capabilities, and example prompts |
| [3.7 — Test Scripts](./3.7_Test_Scripts.md) | Validation scenarios after provisioning |
| [3.8 — Support Contact](./3.8_Support_Contact.md) | Support channels and useful resources |

## How to Navigate

1. Complete the system-level prerequisites in [2_Prepare](../../2_Prepare/).
2. Follow [3.1](./3.1_Provisioning_in_SAP4Me.md) to activate the assistant in SAP for Me.
3. Run [3.2](./3.2_Post-Provisioning_Validations.md) to verify BTP and CIS configuration.
4. Review the individual agent files to understand what each agent can do and test with the provided example prompts.
5. Run validation scenarios from [3.7 — Test Scripts](./3.7_Test_Scripts.md).
