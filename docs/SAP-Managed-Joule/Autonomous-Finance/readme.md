# SAP Autonomous Finance — DC Mission

This directory contains the DC Mission documentation for **SAP Autonomous Finance** — a suite of AI-powered assistants built on Joule that automate finance and sales operations processes across SAP S/4HANA Cloud.

## Structure

The `1_Discover` and `2_Prepare` phases are **shared across all assistants** — they cover SAP Autonomous Finance as a whole. The provisioning phases contain one subfolder per assistant.

```
Autonomous-Finance/
├── 1_Discover/                              # What is SAP Autonomous Finance (shared)
├── 2_Prepare/                               # Prerequisites that apply to all assistants (shared)
├── Public-Cloud-<Assistant-Name>/           # Provisioning steps — SAP S/4HANA Cloud Public Edition
└── Private-Cloud-<Assistant-Name>/          # Provisioning steps — SAP S/4HANA Cloud Private Edition
```

## Assistants

The specific agents available within each assistant may differ between SAP S/4HANA Cloud Public Edition and SAP S/4HANA Cloud Private Edition.

| Assistant | SAP S/4HANA Cloud Public Edition | SAP S/4HANA Cloud Private Edition |
|-----------|-------------|---------------------|
| [Financial Closing Assistant (Public)](./Public-Cloud-Financial-Closing-Assistant/) / [PCE](./Private-Cloud-Financial-Closing-Assistant/) | Available | Available |
| International Trade Assistant | Available | — |
| Financial Consolidation Assistant | Available | — |
| Tax and Compliance Assistant | Available | — |
| [Accounts Payable Assistant (Public)](./Public-Cloud-Accounts-Payable-Assistant/) / [PCE](./Private-Cloud-Accounts-Payable-Assistant/) | Available | Available |
| Billing Assistant | Available | — |
| [Recurring Receivables Assistant (PCE)](./Private-Cloud-Recurring-Receivables-Assistant/) | — | Available |
| [Sales Operations Assistant (PCE)](./Private-Cloud-Sales-Operation-Assistant/) | — | Available |
| [Accounts Receivable Assistant (Public)](./Public-Cloud-Accounts-Receivable-Assistant/) / [PCE](./Private-Cloud-Accounts-Receivable-Assistant/) | Available | Available |
| [Cash and Treasury Assistant (Public)](./Public-Cloud-Cash-and-Treasury-Assistant/) / [PCE](./Private-Cloud-Cash-and-Treasury-Assistant/) | Available | Available |

## How to Navigate

1. Start with **[1_Discover](./1_Discover/)** to understand what SAP Autonomous Finance is and what assistants are available.
2. Review **[2_Prepare](./2_Prepare/)** for prerequisites that apply across all assistants.
3. Open the folder for the assistant you are activating — `Public-Cloud-<AssistantName>` for Public Edition, `Private-Cloud-<AssistantName>` for PCE.
