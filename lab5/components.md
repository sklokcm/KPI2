## Діаграма компонентів
@startuml
left to right direction
skinparam componentStyle rectangle
skinparam linetype ortho
skinparam shadowing false
hide stereotype

title Компоненти системи онлайн-магазину

package "System" {
  () "HTTP/HTTPS API" as PublicAPI

  package "UI" as UIPackage {
    component "Web UI" as WebUI
  }

  package "Backend" {
    package "API Gateway\n(Controllers)" as APIPackage {
      component "AuthController" as AuthController
      component "PaymentMethodController" as PaymentMethodController
    }

    package "Services" as ServicesPackage {
      component "OrderService" as OrderService
      component "AuthService" as AuthService
      component "StorageService" as StorageService
      component "PromoService" as PromoService
      component "PaymentService" as PaymentService
      component "NotificationService" as NotificationService
    }

    package "Data Access\n(Repositories)" as RepositoriesPackage {
      component "UserRepository" as UserRepository
      component "PaymentRepository" as PaymentRepository
      component "OrderRepository" as OrderRepository
      component "StorageRepository" as StorageRepository
    }
  }

  () "SQL" as SQLContract
  database "Database" as Database {
    portout SQLout
  }
}

package "External Integrations" {
  component "PaymentGateway" as PaymentGateway
  component "DeliveryService API" as DeliveryService
  component "Email" as Email
  component "Google SSO service" as GoogleSSO
}

' Контракти між UI, бекендом та базою даних
WebUI ..> PublicAPI
PublicAPI -- AuthController
PublicAPI -- PaymentMethodController

RepositoriesPackage ..> SQLContract
Database::SQLout -- SQLContract

' Controller -> Service
AuthController ..> AuthService
PaymentMethodController ..> PaymentService

' Service -> Repository
AuthService ..> UserRepository
PaymentService ..> PaymentRepository
OrderService ..> OrderRepository
StorageService ..> StorageRepository

' Зовнішні інтеграції
AuthService ..> GoogleSSO
PaymentService ..> PaymentGateway
OrderService ..> DeliveryService
NotificationService ..> Email

' Приховані зв'язки тримають шари стопкою
UIPackage -[hidden]down- APIPackage
APIPackage -[hidden]down- ServicesPackage
ServicesPackage -[hidden]down- RepositoriesPackage
RepositoriesPackage -[hidden]down- Database

@enduml


