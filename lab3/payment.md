@startuml
title Оплата замовлення

actor "Користувач" as User
participant "Сервіс замовлень\n(OrderService)" as OrderService
participant "Promo service" as Promo
participant "Payment service" as Payment
participant "API служби доставки" as Delivery
database "База даних системи" as Database

User -> OrderService : requestPaymentOptions(orderId)
activate OrderService
OrderService --> User : paymentOptions(online, cashOnDelivery)

opt Користувач застосовує промокод
    User -> OrderService : submitPromoCode(orderId, code)
    OrderService -> Promo : validatePromoCode(code, orderId)
    activate Promo
    Promo --> OrderService : promoValidationResult
    deactivate Promo

    alt Промокод дійсний
        OrderService -> Database : applyDiscount(orderId, discount)
        activate Database
        Database --> OrderService : updatedTotalPrice
        deactivate Database
        OrderService --> User : promoApplied(updatedTotalPrice)
    else Промокод недійсний
        OrderService --> User : promoRejected(reason)
    end
end

User -> OrderService : selectPaymentMethod(orderId, method)

alt Онлайн-оплата
    OrderService --> User : requestPaymentDetails()
    User -> OrderService : submitPaymentDetails(paymentDetails)
    OrderService -> Payment : processPayment(orderId, paymentDetails)
    activate Payment
    Payment --> OrderService : paymentConfirmed(orderId)
    deactivate Payment

    OrderService -> Database : updateOrderStatus(orderId, Paid)
    activate Database
    Database --> OrderService : orderStatusUpdated
    deactivate Database
    OrderService --> User : paymentConfirmed(orderId)

else Оплата при отриманні
    OrderService -> Delivery : createShipment(orderId, deliveryAddress, parcelDetails)
    activate Delivery
    Delivery --> OrderService : shipmentCreated(trackingNumber)
    deactivate Delivery
    OrderService --> User : shipmentDetails(trackingNumber)
end

deactivate OrderService
@enduml
![alt text](payment.png)