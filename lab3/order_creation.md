@startuml
title Створення замовлення

actor "Користувач" as User
participant "Сервіс замовлень\n(OrderService)" as OrderService
participant "Сервіс автентифікації\n(AuthService)" as AuthService
participant "Сервіс складу\n(StorageService)" as StorageService
database "База даних системи" as Database

User -> OrderService : createOrder(cartId, deliveryAddress)
activate OrderService
OrderService -> AuthService : checkSession(userId)
activate AuthService
AuthService --> OrderService : sessionStatus(active/inactive)
deactivate AuthService

alt Сесія активна
else Неактивність понад 15 хвилин
    OrderService -> User : requestReauthentication()
    User -> OrderService : submitCredentials(credentials)
    OrderService -> AuthService : authenticate(credentials)
    activate AuthService
    AuthService --> OrderService : authenticationResult
    deactivate AuthService

    alt Автентифікація успішна
    else Автентифікація неуспішна
        break Автентифікацію не пройдено
            OrderService --> User : orderCreationRejected(reason = authentication_failed)
        end
    end
end

loop Для кожної позиції кошика
    OrderService -> StorageService : checkAvailability(productId, quantity)
    activate StorageService
    StorageService --> OrderService : availableQuantity
    deactivate StorageService

    break Запитана кількість недоступна
        OrderService --> User : orderCreationRejected(status = failed, reason = out_of_stock)
    end
end

OrderService -> StorageService : reserveItems(cartItems)
activate StorageService
StorageService --> OrderService : reservationResult
deactivate StorageService

alt Резервування успішне
    OrderService -> Database : createOrder(cartId, deliveryAddress, prices, status = created)
    activate Database
    Database --> OrderService : orderCreated(orderId)
    deactivate Database

    OrderService -> Database : clearCart(cartId)
    activate Database
    Database --> OrderService : cartCleared
    deactivate Database

    OrderService -> Database : updateOrderStatus(orderId, pending)
    activate Database
    Database --> OrderService : orderStatusUpdated
    deactivate Database

    OrderService --> User : orderCreated(orderId, status = pending)
else Резервування неуспішне
    OrderService --> User : orderCreationRejected(status = failed, reason = reservation_failed)
end

deactivate OrderService
@enduml
![alt text](image-1.png)