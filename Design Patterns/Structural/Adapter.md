# Adapter – Toscana RMS

```mermaid
classDiagram
    class KitchenCoordinator {
        +showOrderToKitchen(order: String)
        -display: KitchenDisplay
    }

    class KitchenDisplay {
        <<interface>>
        +displayOrder(order: String)
    }

    class OldKitchenScreen {
        +showOnScreen(data: String)
    }

    class KitchenDisplayAdapter {
        -oldScreen: OldKitchenScreen
        +displayOrder(order: String)
    }

    KitchenCoordinator --> KitchenDisplay : uses
    KitchenDisplayAdapter ..|> KitchenDisplay : implements
    KitchenDisplayAdapter --> OldKitchenScreen : adapts
