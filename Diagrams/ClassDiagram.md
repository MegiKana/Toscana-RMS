Class Diagram 
```mermaid
classDiagram

%% === Entities with Attributes ===

class Customer {
  +String customerID
  +String name
  +String email
  +String phone
  +String preferences
  +int loyaltyPoints
}

class Reservation {
  +String reservationID
  +String status
  +DateTime dateTime
}

class Table {
  +String tableID
  +int tableNumber
  +int seats
  +String location
}

class Order {
  +String orderID
  +DateTime dateTime
}

class MenuItem {
  +String menuItemID
  +String name
  +String description
  +float price
}

class OrderItem {
  +int quantity
}

class Feedback {
  +String feedbackID
  +String content
}

class Waiter {
  +String waiterID
  +String name
  +String email
  +String phone
  +String role
}

class KitchenStaff {
  +String staffID
  +String name
  +String role
  +String shiftDetails
}

class Payment {
  +String paymentID
  +String method
  +float amount
}

class Manager {
  +String managerID
  +String name
  +String contactInfo
}

class Supplier {
  +String supplierID
  +String name
  +String contactInfo
}

class Inventory {
  +String inventoryID
  +String itemName
  +int quantity
  +Date lastUpdate
  +int reorder
}


%% === Relationships from ERD ===

Customer "1" --> "0..*" Reservation : makes
Reservation "1" --> "1" Customer : made by
Reservation "1" --> "1" Table : assigned
Customer "1" --> "0..*" Order : places
Order "1" --> "1" Customer : belongs to
Order "1" --> "0..*" OrderItem : contains
MenuItem "1" --> "0..*" OrderItem : appears in
OrderItem "1" --> "1" Order : part of
OrderItem "1" --> "1" MenuItem : for item
Order "1" --> "1" Payment : paid by
Order "1" --> "0..1" Feedback : rated by
Feedback "1" --> "1" Customer : given by
Feedback "1" --> "1" Order : about
Order "1" --> "1" Waiter : served by
KitchenStaff "1" --> "0..*" MenuItem : prepares
MenuItem "0..*" --> "1" KitchenStaff : prepared by
Manager "1" --> "0..*" Waiter : oversees
Inventory "1" --> "0..*" MenuItem : supplies
Inventory "1" --> "1" Supplier : supplied by
Supplier "1" --> "0..*" Inventory : provides

