# SAP Autonomous Finance — DC Mission

This directory contains the DC Mission documentation for **SAP Autonomous Finance** assistants powered by Joule.

## Structure

```
Autonomous-Finance/
├── 1_Discover/                              # General discovery content (all assistants)
├── 2_Prepare/                               # General prerequisites (all assistants)
├── 3_Assistant-Provisioning-1-Public/       # Provisioning for SAP S/4HANA Cloud Public Edition
│   └── <Assistant-Name>/                    # One subfolder per assistant
└── 4_Assistant-Provisioning-1-PCE/          # Provisioning for SAP S/4HANA Cloud Private Edition
    └── <Assistant-Name>/                    # One subfolder per assistant
```

## Assistants

| Assistant | Public Cloud | Private Cloud (PCE) |
|-----------|-------------|---------------------|
| [Sales Operation Assistant](./4_Assistant-Provisioning-1-PCE/Sales-Operation-Assistant/) | Planned | Available |
| Financial Closing Assistant | Planned | Planned |
| Accounts Payable Assistant | Planned | Planned |
| Accounts Receivable Assistant | Planned | Planned |
| Recurring Receivables Assistant | Planned | Planned |
| Cash and Treasury Assistant | Planned | Planned |

## How to Navigate

- Start with **1_Discover** for an overview of SAP Autonomous Finance and the available assistants.
- Review **2_Prepare** for prerequisites that apply across all assistants.
- Go to the relevant provisioning phase folder (**3** for Public Cloud, **4** for PCE) and open the subfolder for the assistant you are activating.
