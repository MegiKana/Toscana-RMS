# Data Flow Diagram Level 2

```mermaid
flowchart TD
    %% External Entities
    Customers[Customers]:::entity
    Staff[Restaurant Staff]:::entity
    Kitchen[Kitchen Staff]:::entity
    
    %% Data Stores
    DB1[Order Database]:::datastore
    DB2[Menu Database]:::datastore
    DB3[Inventory Database]:::datastore
    
    %% Level 2 Processes for Order Management
    P2.1((2.1 Take\Customer Order)):::process
    P2.2((2.2 Validate\Order Items)):::process
    P2.3((2.3 Create\Kitchen Ticket)):::process
    P2.4((2.4 Monitor\Order Status)):::process
    P2.5((2.5 Generate\Bill)):::process
    
    %% Data Flows - Customer Order Entry
    Customers -->|Order request| P2.1
    Staff -->|Enter order details| P2.1
    P2.1 -->|Order items| P2.2
    P2.1 -->|Store order| DB1
    
    %% Data Flows - Menu and Inventory Validation
    P2.2 <-->|Check menu items| DB2
    P2.2 <-->|Check ingredient availability| DB3
    P2.2 -->|Validated order| P2.3
    
    %% Data Flows - Kitchen Operations
    P2.3 -->|Kitchen ticket| Kitchen
    P2.3 -->|Update order status| DB1
    Kitchen -->|Preparation updates| P2.4
    
    %% Data Flows - Order Status Management
    P2.4 <-->|Retrieve/Update status| DB1
    P2.4 -->|Order status| Staff
    P2.4 -->|Ready for billing| P2.5
    P2.4 -->|Update inventory| DB3
    
    %% Data Flows - Billing
    P2.5 <-->|Order details| DB1
    P2.5 -->|Bill| Customers
    
    classDef entity fill:#f8d7da,stroke:#721c24,stroke-width:1px;
    classDef process fill:#cce5ff,stroke:#004085,stroke-width:1px,border-radius:50px;
    classDef datastore fill:#d1ecf1,stroke:#0c5460,stroke-width:1px;
