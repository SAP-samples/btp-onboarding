# SAP Autonomous Finance — DC Mission

This directory contains the DC Mission documentation for **SAP Autonomous Finance** — a suite of AI-powered assistants built on Joule that automate finance and sales operations processes across SAP S/4HANA Cloud.

## Structure

The `1_Discover` and `2_Prepare` phases are **shared across all assistants** — they cover SAP Autonomous Finance as a whole. The provisioning phases contain one subfolder per assistant.

```
Autonomous-Finance/
├── 1_Discover/                              # What is SAP Autonomous Finance (shared)
├── 2_Prepare/                               # Prerequisites that apply to all assistants (shared)
├── 3_Assistant-Provisioning-1-Public/       # Provisioning steps for SAP S/4HANA Cloud Public Edition
│   └── <Assistant-Name>/                    # One subfolder per assistant
└── 4_Assistant-Provisioning-1-PCE/          # Provisioning steps for SAP S/4HANA Cloud Private Edition
    └── <Assistant-Name>/                    # One subfolder per assistant
```

## Assistants

The specific agents available within each assistant may differ between SAP S/4HANA Cloud Public Edition and SAP S/4HANA Cloud Private Edition.

| Assistant | SAP S/4HANA Cloud Public Edition | SAP S/4HANA Cloud Private Edition |
|-----------|-------------|---------------------|
| [Sales Operations Assistant](./4_Assistant-Provisioning-1-PCE/Sales-Operation-Assistant/) | — | Available |
| [Financial Closing Assistant (Public)](./3_Assistant-Provisioning-1-Public/Financial-Closing-Assistant/) / [PCE](./4_Assistant-Provisioning-1-PCE/Financial-Closing-Assistant/) | Available | Available |
| [Accounts Receivable Assistant (Public)](./3_Assistant-Provisioning-1-Public/Accounts-Receivable-Assistant/) / [PCE](./4_Assistant-Provisioning-1-PCE/Accounts-Receivable-Assistant/) | Available | Available |
| [Recurring Receivables Assistant](./4_Assistant-Provisioning-1-PCE/Recurring-Receivables-Assistant/) | — | Available |
| [Accounts Payable Assistant (Public)](./3_Assistant-Provisioning-1-Public/Accounts-Payable-Assistant/) / [PCE](./4_Assistant-Provisioning-1-PCE/Accounts-Payable-Assistant/) | Available | Available |
| [Cash and Treasury Assistant (Public)](./3_Assistant-Provisioning-1-Public/Cash-and-Treasury-Assistant/) / [PCE](./4_Assistant-Provisioning-1-PCE/Cash-and-Treasury-Assistant/) | Available | Available |
| Financial Consolidation Assistant | Available | — |
| Tax and Compliance Assistant | Available | — |
| Governance, Risk, and Compliance Assistant | Available | — |

## How to Navigate

1. Start with **[1_Discover](./1_Discover/)** to understand what SAP Autonomous Finance is and what assistants are available.
2. Review **[2_Prepare](./2_Prepare/)** for prerequisites that apply across all assistants.
3. Go to the relevant provisioning phase (**3** for Public Cloud, **4** for PCE) and open the subfolder for the assistant you are activating.
