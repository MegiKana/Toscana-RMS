Class Diagram 
```mermaid
classDiagram
direction LR
%% === Customer and Reservation System ===
class Customer {
    +String name
    +String phone
    +String email
    +makeReservation()
    +modifyReservation()
    +cancelReservation()
    +makeOrder()
    +redeemLoyaltyPoints()
    +provideFeedback()
}

class Reservation {
    +int reservationId
    +Date date
    +Time time
    +int tableNumber
    +String status
    +confirmReservation()
    +updateReservation()
    +cancelReservation()
}

class Table {
    +int tableNumber
    +int capacity
    +boolean isAvailable
    +checkAvailability()
}

class LoyaltyReward {
    +int points
    +String rewardType
    +redeem()
}

Customer "1" --> "0..*" Reservation : makes
Reservation "1" --> "1" Table : assigned to
Customer "1" --> "0..1" LoyaltyReward : earns

%% === Ordering and Kitchen Workflow ===
class MenuItem {
    +int itemId
    +String name
    +double price
    +boolean available
}

class Order {
    +int orderId
    +DateTime time
    +double totalPrice
    +placeOrder()
    +splitGroupOrder()
}

class OrderItem {
    +int quantity
    +double subtotal
}

class Waiter {
    +String name
    +inputOrder()
    +serveOrder()
    +suggestAlternative()
}

class KitchenStaff {
    +String name
    +updateOrderStatus()
    +flagUnavailableItem()
}

Customer "1" --> "0..*" Order : places
Order "1" -- "1.." OrderItem : composed of
OrderItem "1" --> "1" MenuItem : refers to
Waiter "1" --> "0..*" Order : manages
KitchenStaff "1" --> "0..*" Order : updates

%% === Inventory and Stock ===
class InventoryItem {
    +int itemId
    +String name
    +int quantity
    +String supplier
    +updateStockLevel()
    +checkLowStock()
}

class InventoryReport {
    +generateDailyReport()
    +generateWeeklyReport()
}

class RestockOrder {
    +int orderId
    +Date orderDate
    +placeRestockingOrder()
}

class Manager {
    +String name
}

Manager "1" --> "0..*" InventoryReport : views
Manager "1" --> "0..*" RestockOrder : places
InventoryItem "1" --> "0..*" RestockOrder : triggers

%% === Employee Management ===
class Employee {
    +String name
    +String role
}

class Shift {
    +Date date
    +Time startTime
    +Time endTime
    +assignShift()
}

class Admin {
    +assignShifts()
    +reviewScheduleChange()
}

class Staff {
    +requestScheduleChange()
}

Admin "1" --> "0..*" Shift : assigns
Staff "1" --> "0..*" Shift : requests
Manager "1" --> "0..*" Employee : manages
Manager "1" --> "0..*" Shift : tracks

%% === Feedback and Reports ===
class Feedback {
    +String comments
    +int rating
    +DateTime submittedOn
}

Customer "1" --> "0..*" Feedback : submits

%% === System and Notification ===
class System {
    +checkTableAvailability()
    +sendNotification()
    +processDeliveryOrder()
    +highlightPaymentIssues()
}

System --> Table : checks availability
System --> Staff : notifies
System --> Order : processes delivery
