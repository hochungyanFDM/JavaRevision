# Institutional trade lifecycle

## 1. Trade date — order to booking

```mermaid
flowchart TD
    A["PM / trader places order<br/><i>via OMS / EMS</i>"]
    B["Executing broker / venue<br/><i>algo, exchange, dark pool</i>"]
    C["Fills come back<br/><i>FIX execution reports / drop copy</i>"]
    D["Trade capture / booking<br/><i>fills aggregated, average price</i>"]
    E["Enrichment + allocation<br/><i>split block across funds / accounts</i>"]

    A --> B --> C --> D --> E

    style A fill:#EEEDFE,stroke:#534AB7,color:#3C3489
    style B fill:#EEEDFE,stroke:#534AB7,color:#3C3489
    style C fill:#EEEDFE,stroke:#534AB7,color:#3C3489
    style D fill:#E1F5EE,stroke:#0F6E56,color:#085041
    style E fill:#E1F5EE,stroke:#0F6E56,color:#085041
```

Purple = front office · Green = middle office

## 2. Post-trade flow

```mermaid
flowchart TD
    F["Downstream systems<br/><i>PB (give-up), custodian, accounting, risk</i>"]
    G["Confirm / affirm / match<br/><i>DTCC CTM, TradeSuite ID (US)</i>"]
    H["Clearing<br/><i>nets obligations between parties</i>"]
    I["Settlement<br/><i>cash and securities move (US T+1)</i>"]
    J["Reconciliation<br/><i>internal vs PB / custodian / accounting</i>"]
    K["Breaks / exceptions<br/><i>mismatches investigated by ops</i>"]

    F --> G --> H --> I --> J --> K

    style F fill:#E1F5EE,stroke:#0F6E56,color:#085041
    style G fill:#E1F5EE,stroke:#0F6E56,color:#085041
    style H fill:#E1F5EE,stroke:#0F6E56,color:#085041
    style I fill:#E1F5EE,stroke:#0F6E56,color:#085041
    style J fill:#E1F5EE,stroke:#0F6E56,color:#085041
    style K fill:#FAECE7,stroke:#993C1D,color:#712B13
```

## 3. DTCC CTM — confirmation and affirmation (US, T+1)

```mermaid
flowchart TD
    L["Executing broker<br/><i>submits confirmation</i>"]
    M["Buy-side / fund<br/><i>submits trade + allocations</i>"]
    N["CTM central matching<br/><i>compares both versions field by field</i>"]
    O["Affirmation<br/><i>TradeSuite ID, M2i auto-affirm, 9pm ET on T</i>"]
    P["DTC settlement<br/><i>settles T+1</i>"]

    L --> N
    M --> N
    N --> O --> P

    style L fill:#EEEDFE,stroke:#534AB7,color:#3C3489
    style M fill:#EEEDFE,stroke:#534AB7,color:#3C3489
    style N fill:#E1F5EE,stroke:#0F6E56,color:#085041
    style O fill:#E1F5EE,stroke:#0F6E56,color:#085041
    style P fill:#F1EFE8,stroke:#5F5E5A,color:#2C2C2A
```

## Key points

- **Execution vs prime brokerage**: orders go to executing brokers/venues; trades executed away are *given up* to the PB, which handles custody, financing, margin, stock borrow, and settlement support.
- **Fill aggregation**: multiple fills may be booked as one average-price trade or kept as fill-level records, depending on booking logic.
- **T+1 (US, May 2024)**: allocation, confirmation, and affirmation must complete on trade date. DTC affirmation cutoff is 9:00 PM ET on T (SEC Rule 15c6-2 requires same-day affirmation agreements). For APAC funds this cutoff lands the next morning local time, making overnight automation critical.
- **Breaks**: reconciliation mismatches between internal records and PB/custodian/accounting records, investigated and resolved by ops/support.
