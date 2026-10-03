# State Machine Diagram

```mermaid
---
title: State Machine Diagram
---
stateDiagram-v2
    direction LR
    [*] --> Pending : Member Registration
    Pending --> Active : Staff Approves Record
    Active --> Inactive : Staff Deactivates Record
    Inactive --> Pending : Member Re-registers
    Active --> [*] : Record Archived
    Inactive --> [*] : Record Archived
```
