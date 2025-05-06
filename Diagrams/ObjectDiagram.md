Object Diagram
```mermaid
classDiagram
    class Customer {
        +customerId: 101
        +name: "Sarah Parker"
        +email: "sarah.parker@gmail.com"
        +phoneNumber: "+1234567890"
        +address: "123 Main St, Springfield"
        +placeOrder(): Order
        +cancelReservation(): void
    }

    class Reservation {
        +reservationId: 202
        +date: "2025-05-06"
        +time: "19:00"
        +status: "Confirmed"
        +createReservation(): void
        +cancelReservation(): void
    }

    class Table {
        +tableId: 301
        +capacity: 4
        +isAvailable: true
        +reserveTable(): void
        +releaseTable(): void
    }

    class Order {
        +orderId: 401
        +orderDate: "2025-05-06"
        +status: "In Progress"
        +addItem(menuItem: MenuItem, quantity: 2): void
        +removeItem(menuItem: MenuItem): void
        +calculateTotal(): float
    }

    class OrderItem {
        +orderItemId: 501
        +quantity: 2
        +price: 15.99
        +menuItem: MenuItem
        +totalPrice(): float
    }

    class MenuItem {
        +menuItemId: 601
        +name: "Spaghetti Carbonara"
        +description: "Classic Italian pasta with eggs, cheese, pancetta, and pepper."
        +price: 15.99
        +category: "Main Course"
    }

    Customer "1" -- "0..*" Order : places
    Order "1" -- "1..*" OrderItem : contains
    MenuItem "1" -- "0..*" OrderItem : is part of
    Reservation "1" -- "1..*" Table : reserves
    Table "1" -- "0..1" Reservation : is reserved by
    Customer "1" -- "0..1" Reservation : makes
