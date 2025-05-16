Class Diagram 
```mermaid
classDiagram

%% ==== MAIN ACTORS ====
class Customer {
  +String customerID
  +String name
  +String email
  +String phone
  +String preferences
  +int loyaltyPoints
  +placeReservation()
  +placeOrder()
  +giveFeedback()
}

class Reservation {
  +String reservationID
  +String status
  +String dateTime
  +makeReservation()
  +cancelReservation()
}

class Table {
  +String tableID
  +int tableNumber
  +int seats
  +String location
  +assignReservation()
}

class Feedback {
  +String feedbackID
  +String content
  +rateExperience()
}

class Order {
  +String orderID
  +String dateTime
  +placeOrder()
  +calculateTotal()
}

class OrderItem {
  +int quantity
}

class MenuItem {
  +String menuItemID
  +String name
  +double price
  +String description
}

class Waiter {
  +String waiterID
  +String name
  +String email
  +String phone
  +String role
  +serveOrder()
}

class KitchenStaff {
  +String staffID
  +String name
  +String role
  +String shiftDetails
  +prepareItem()
}

class Manager {
  +String managerID
  +String name
  +String contactInfo
  +overseeOperations()
}

class Payment {
  +String paymentID
  +double amount
  +String method
  +String dateTime
  +makePayment()
}

class Supplier {
  +String supplierID
  +String name
  +String contactInfo
  +supplyItems()
}

class Inventory {
  +String inventoryID
  +String itemName
  +int quantity
  +String lastUpdate
  +int reorderLevel
  +updateInventory()
}

%% ==== RELATIONSHIPS ====
Customer "1" --> "*" Reservation : makes
Customer "1" --> "*" Feedback : gives
Customer "1" --> "*" Order : places
Reservation "1" --> "1" Table : assignedTo
Reservation "1" --> "1" Customer : by
Order "1" --> "*" OrderItem : contains
OrderItem "*" --> "1" MenuItem : includes
Order "1" --> "1" Waiter : servedBy
Order "1" --> "1" Payment : paidWith
Feedback "1" --> "1" Customer : by
Inventory "1" --> "1" Supplier : suppliedBy
Inventory "1" --> "*" MenuItem : usedFor
KitchenStaff "1" --> "*" MenuItem : prepares
Manager "1" --> "*" Payment : oversees
Manager "1" --> "*" Staff : manages

%% Optional abstraction if desired
class Staff {
  +String staffID
  +String name
  +String role
}
Staff <|-- Waiter
Staff <|-- KitchenStaff
