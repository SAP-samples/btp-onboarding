# Accounts Receivable Assistant — Public Cloud Provisioning

This directory contains the provisioning documentation for the **Accounts Receivable Assistant** on **SAP S/4HANA Cloud Public Edition**.

## About this Assistant

The Accounts Receivable Assistant supports AR accountants and collection specialists by automating dispute analysis, optimising collections outreach, and delivering intelligent receivable insights. It uses an orchestration agent that dispatches requests to specialised sub-agents covering the full range of daily AR activities.

## Agents in this Assistant

| Agent | Purpose |
|-------|---------|
| Accounts Receivable Orchestration Agent | Routes requests to the appropriate AR sub-agents across collections, disputes, dunning, and clearing |
| Receivable Account Analysis Agent | Provides an in-depth overview of a customer's receivable health across invoices, disputes, and credit memos |
| Collection Account Preparation Agent | Consolidates and analyses collection account data to prepare collection specialists for customer outreach |
| Collections Email Outreach Agent | Generates and sends personalised collections emails in the customer's preferred language |
| Dunning Insights Agent | Analyses dunning history and levels, identifies risk, and provides actionable recommendations |
| Dispute Creation Agent | Creates dispute cases from billing documents and unstructured inputs such as user prompts and emails |
| Dispute Resolution Agent | Retrieves comprehensive dispute data, validates claims, and provides tailored resolution recommendations |

## Mission Structure

| File | Content |
|------|---------|
| [3.1 — Provisioning in SAP for Me](./3.1_Provisioning_in_SAP4Me.md) | Step-by-step activation wizard in SAP for Me |
| [3.2 — Post-Provisioning Validations](./3.2_Post-Provisioning_Validations.md) | BTP resources, formation, and CIS groups validation |
| [3.3 — Receivable Account Analysis Agent](./3.3_Receivable_Account_Analysis_Agent.md) | Objective, capabilities, and example prompts |
| [3.4 — Collection Account Preparation Agent](./3.4_Collection_Account_Preparation_Agent.md) | Objective, capabilities, and example prompts |
| [3.5 — Collections Email Outreach Agent](./3.5_Collections_Email_Outreach_Agent.md) | Objective, capabilities, and example prompts |
| [3.6 — Dunning Insights Agent](./3.6_Dunning_Insights_Agent.md) | Objective, capabilities, and example prompts |
| [3.7 — Dispute Creation Agent](./3.7_Dispute_Creation_Agent.md) | Objective, capabilities, and example prompts |
| [3.8 — Dispute Resolution Agent](./3.8_Dispute_Resolution_Agent.md) | Objective, capabilities, and example prompts |
| [3.9 — Test Scripts](./3.9_Test_Scripts.md) | Validation scenarios after provisioning |
| [3.10 — Support Contact](./3.10_Support_Contact.md) | Support channels and useful resources |

## How to Navigate

1. Complete the system-level prerequisites in [2_Prepare](../../2_Prepare/).
2. Follow [3.1](./3.1_Provisioning_in_SAP4Me.md) to activate the assistant in SAP for Me.
3. Run [3.2](./3.2_Post-Provisioning_Validations.md) to verify BTP and CIS configuration.
4. Review the individual agent files to understand what each agent can do and test with the provided example prompts.
5. Run validation scenarios from [3.9 — Test Scripts](./3.9_Test_Scripts.md).
