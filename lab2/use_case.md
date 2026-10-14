```mermaid
flowchart LR
    User[Користувач]
    Manager[Менеджер]
    SupportManager[Менеджер підтримки]
    Administrator[Адміністратор]
    Delivery[Служба доставки]
    Payment[Сервіс оплати]

    Manager ---|спеціалізація| SupportManager
    Manager ---|спеціалізація| Administrator

    subgraph System[Система електронної комерції]
        UC1[Реєстрація користувача]
        UC2[Авторизація в системі]
        UC3[Відновлення пароля]
        UC4[Керування кошиком]
        UC5[Оформлення замовлення]
        UC6[Перевірка наявності товарів]
        UC7[Бронювання товарів]
        UC8[Створення платежу]
        UC9[Оплата замовлення]
        UC10[Оплата онлайн]
        UC11[Оплата при отриманні]
        UC12[Застосування промокоду]
        UC13[Перегляд статусу замовлення]
        UC14[Створення звернення в підтримку]
        UC15[Обробка звернення підтримкою]
        UC16[Керування товарами та категоріями]
        UC17[Передача замовлення службі доставки]
    end

    User --> UC1
    User --> UC2
    User --> UC3
    User --> UC4
    User --> UC5
    User --> UC13
    User --> UC14

    SupportManager --> UC15
    Administrator --> UC16
    Manager --> UC17

    UC5 -. includes .-> UC6
    UC5 -. includes .-> UC7
    UC5 -. includes .-> UC8
    UC5 -. includes .-> UC9
    UC10 ---|спеціалізація| UC9
    UC11 ---|спеціалізація| UC9
    UC12 -. extends .-> UC5

    UC17 --> Delivery
    UC10 --> Payment
```
