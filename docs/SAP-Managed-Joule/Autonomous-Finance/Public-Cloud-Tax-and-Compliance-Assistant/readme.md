# Tax and Compliance Assistant — Public Cloud Provisioning

This directory contains the provisioning documentation for the **Tax and Compliance Assistant** on **SAP S/4HANA Cloud Public Edition**.

## About this Assistant

The Tax and Compliance Assistant helps tax specialists and compliance teams manage regulatory changes, understand document-to-report field mappings, and maintain statutory report extensions. It uses an orchestration agent that dispatches requests to specialised sub-agents covering legal change discovery, regulatory document mapping, and statutory report management.

## Agents in this Assistant

| Agent | Purpose |
|-------|---------|
| Tax and Compliance Orchestration Agent | Coordinates the specialised agents within the Tax and Compliance Assistant |
| Legal Change Agent | Enables regulatory compliance discovery for customers |
| Regulatory Document Mapping Explanation Agent | Explains field-level mappings between source data, SAP documents, and e-invoicing or statutory reporting formats |
| Statutory Report Extension Update Agent | Merges customer extensions when SAP releases new statutory report versions, reducing manual work |

## Works With

| Agent | Platform |
|-------|---------|
| Tax and Compliance Orchestration Agent | SAP S/4HANA Cloud Public Edition, SAP Document and Reporting Compliance |
| Legal Change Agent | SAP S/4HANA Cloud Public Edition |
| Regulatory Document Mapping Explanation Agent | SAP S/4HANA Cloud Public Edition, SAP Document and Reporting Compliance |
| Statutory Report Extension Update Agent | SAP S/4HANA Cloud Public Edition |

## Mission Structure

| File | Content |
|------|---------|
| [3.1 — Provisioning in SAP for Me](./3.1_Provisioning_in_SAP4Me.md) | Step-by-step activation wizard in SAP for Me |
| [3.2 — Post-Provisioning Validations](./3.2_Post-Provisioning_Validations.md) | BTP resources, formation, and CIS groups validation |
| [3.3 — Tax and Compliance Orchestration Agent](./3.3_Tax_and_Compliance_Orchestration_Agent.md) | Objective, sub-agents coordinated, and example prompts |
| [3.4 — Legal Change Agent](./3.4_Legal_Change_Agent.md) | Objective, capabilities, and example prompts |
| [3.5 — Regulatory Document Mapping Explanation Agent](./3.5_Regulatory_Document_Mapping_Explanation_Agent.md) | Objective, capabilities, and example prompts |
| [3.6 — Statutory Report Extension Update Agent](./3.6_Statutory_Report_Extension_Update_Agent.md) | Objective, capabilities, and example prompts |
| [3.7 — Test Scripts](./3.7_Test_Scripts.md) | Validation scenarios after provisioning |
| [3.8 — Support Contact](./3.8_Support_Contact.md) | Support channels and useful resources |

## How to Navigate

1. Complete the system-level prerequisites in [2_Prepare](../../2_Prepare/).
2. Follow [3.1](./3.1_Provisioning_in_SAP4Me.md) to activate the assistant in SAP for Me.
3. Run [3.2](./3.2_Post-Provisioning_Validations.md) to verify BTP and CIS configuration.
4. Review the individual agent files to understand what each agent can do and test with the provided example prompts.
5. Run validation scenarios from [3.7 — Test Scripts](./3.7_Test_Scripts.md).
