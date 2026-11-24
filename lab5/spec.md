## Намір
* Створити діаграму компонентів усієї системи.

## Критерії
* Діаграма повинна узгоджуватися з вимогами, моделлю даних, взаємодією та процесом.
* Зовнішні інтеграції - усе, що в Use Case дфаграмі зображувалося як зовнішні системи
* Підхід - горизонтальні шари: Пакет = шар; структура UI -> API(controlers) -> Services -> Data Access(repositories) -> DB; жодних залежностей вгору; контракти(lollipop) лише на межі системи і на базу даних; одна спільна схема БД.
* Діаграма має бути охайною: вирівняні шари і модулі, мінімум перетинів, читабельні підписи. Використовувати -up-, -down-, -left-, -right- і приховані зв'язки, що тримають шари стопкою.

## Шари і компоненти
### Внутрішні компоненти
1. Web UI
2. API Gateway(controlers)
* AuthController
* PaymentMethodController
3. Services
* OrderService
* AuthService
* StorageService
* PromoService
* PaymentService
* NotificationService
4. Data access(Repositories)
* UserRepository
* PaymentRepository
* OrderRepository
* StorageRepository
5. Data Base
### Зовнішні ігтеграції 
1. PaymentGateway
2. DeliveryService API
3. Email
4. Google SSO service
## Залежності/Зв'язки
* Пакети API, Services, Data Access межі Backend, WebUI та БД за межами бекенду, але в System.
* Controller -> Service -> Repository пукнтрирною стрілкою. 
* Порт SQlout до Бази даних, зв'язок lollipop.
