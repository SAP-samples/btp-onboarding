# Financial Closing Assistant — PCE Provisioning

This directory contains the provisioning documentation for the **Financial Closing Assistant** on **SAP S/4HANA Cloud Private Edition**.

## About this Assistant

The Financial Closing Assistant supports finance teams to manage the period close. It uses an orchestration agent that dispatches requests to specialised sub-agents, covering journal entry processing, accrual preparation, analytical insights, asset accounting anomaly detection, financial consistency analysis, and clearing activities.

## Agents in this Assistant

| Agent | Purpose |
|-------|---------|
| Financial Closing Orchestration Agent | Dispatches requests to the appropriate sub-agents in the context of financial closing |
| Accounting Accruals Agent | Automates preparation of manual accruals and generates accrual proposals from a policy handbook |
| Analytical Business Insights Agent | Evaluates company-level financial status through KPIs and creates summary analyses |
| Asset Accounting Anomaly Detection Agent | Detects anomalies and inconsistencies in Fixed Asset Accounting (FI-AA) data before period-end close |
| Financial Consistency Analysis Agent | Identifies and corrects data inconsistencies that can prevent clearing processes |
| Journal Entry Agent | Automates and simplifies the creation of journal entries from uploaded spreadsheet data |
| Receivables and Payables Clearing Agent | Automatically generates clearing proposals for open receivable and payable items |

## Mission Structure

| File | Content |
|------|---------|
| [4.1 — Provisioning in SAP for Me](./4.1_Provisioning_in_SAP4Me.md) | Step-by-step activation wizard in SAP for Me |
| [4.2 — Post-Provisioning Validations](./4.2_Post-Provisioning_Validations.md) | BTP resources, formation, and CIS groups validation |
| [4.3 — Accounting Accruals Agent](./4.3_Accounting_Accruals_Agent.md) | Objective, capabilities, and example prompts |
| [4.4 — Analytical Business Insights Agent](./4.4_Analytical_Business_Insights_Agent.md) | Objective, capabilities, and example prompts |
| [4.5 — Asset Accounting Anomaly Detection Agent](./4.5_Asset_Accounting_Anomaly_Detection_Agent.md) | Objective, capabilities, and example prompts |
| [4.6 — Financial Consistency Analysis Agent](./4.6_Financial_Consistency_Analysis_Agent.md) | Objective, capabilities, and example prompts |
| [4.7 — Journal Entry Agent](./4.7_Journal_Entry_Agent.md) | Objective, capabilities, and example prompts |
| [4.8 — Receivables and Payables Clearing Agent](./4.8_Receivables_and_Payables_Clearing_Agent.md) | Objective, capabilities, and example prompts |
| [4.9 — CIS Authorizations / AMS Policies](./4.9_CIS_Authorizations_AMS_Policies.md) | User group assignment in SAP Cloud Identity Services |
| [4.10 — Test Scripts](./4.10_Test_Scripts.md) | Validation scenarios after provisioning |
| [4.11 — Support Contact](./4.11_Support_Contact.md) | Support channels and useful resources |

## How to Navigate

1. Complete the system-level prerequisites in [2_Prepare](../../2_Prepare/).
2. Follow [4.1](./4.1_Provisioning_in_SAP4Me.md) to activate the assistant in SAP for Me.
3. Run [4.2](./4.2_Post-Provisioning_Validations.md) to verify BTP and CIS configuration.
4. Review the individual agent files to understand what each agent can do and test with the provided example prompts.
5. Assign users via [4.9](./4.9_CIS_Authorizations_AMS_Policies.md).
