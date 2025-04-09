# Data Flow Diagram Level 1

```mermaid
flowchart TD
    %% External Entities
    Customers[Customers]:::entity
    Suppliers[Suppliers]:::entity
    Staff[Restaurant Staff]:::entity
    PaymentSystems[Payment Systems]:::entity
    
    %% Processes
    P1((Reservation\Management)):::process
    P2((Order\Management)):::process
    P3((Payment\Processing)):::process
    
    %% Data Stores
    DB1[Reservation\Database]:::datastore
    DB2[Order\Database]:::datastore
    DB3[Payment\Database]:::datastore
    DB4[Inventory\Database]:::datastore
    
    %% Data Flows - Customers
    Customers -->|Reservation\request| P1
    P1 -->|Reservation\confirmation| Customers
    
    %% Data Flows - Reservation Management
    P1 -->|Order\details| P2
    P1 -->|Payment\details| P3
    Staff -->|Order details| DB1
    
    %% Data Flows - Order Management
    Staff -->|Order\status| P2
    P2 -->|Prepared\order| Staff
    P2 -->|Kitchen\requests| DB2
    P2 -->|Inventory\alerts| DB3
    
    %% Data Flows - Payment Processing
    P3 -->|Transaction\confirmation| P2
    P2 -->|Inventory\processing| P3
    
    %% Data Flows - Suppliers
    P1 -->|Restocking\request| Suppliers
    Suppliers -->|Inventory\updates| P1
    Suppliers -->|Payment\processing| P3
    
    %% Additional connections
    P3 -->|Payment\Systems| PaymentSystems
    
    classDef entity fill:#f8d7da,stroke:#721c24,stroke-width:1px;
    classDef process fill:#cce5ff,stroke:#004085,stroke-width:1px,border-radius:50px;
    classDef datastore fill:#d1ecf1,stroke:#0c5460,stroke-width:1px;
