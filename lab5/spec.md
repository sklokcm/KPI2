## Намір
* Створити діаграму компонентів усієї системи.

## Критерії
* Діаграма повинна узгоджуватися з вимогами, моделлю даних, взаємодією та процесом.
* Зовнішні інтеграції - усе, що в Use Case дфаграмі зображувалося як зовнішні системи
* Підхід - горизонтальні шари: Пакет = шар; структура UI -> API(controlers) -> Services -> Data Access(repositories) -> DB; жодних залежностей вгору; контракти(lollipop) лише на межі системи і на базу даних; одна спільна схема БД.
* Діаграма має бути охайною: вирівняні шари і модулі, мінімум перетинів, читабельні підписи. Використовувати -up-, -down-, -left-, -right- і приховані зв'язки, що тримають шари стопкою.
* Пакети API, Services, Data Access межі Backend, WebUI та БД за межами бекенду, але в System.
* External Integraitions поза межами системи, також вони не повинні бути зібрані в один пакет. 
* Controller -> Service -> Repository та залежності всередині одного шару зображати пукнтрирною стрілкою, зв'язки зі сторонніми компонентами суцільною лінією. 

## Шари і компоненти
### Внутрішні компоненти
1. Web UI
2. API(controlers)
* Router
* AuthController
* PaymentMethodController
* PaymentController
* StorageController
* OrderController
* SupportController
* PaymentWebhookController
3. Services
* OrderService
* AuthService
* StorageService
* PromoService
* PaymentService
* NotificationService
* SupportService
4. Data access(Repositories)
* UserRepository
* PaymentRepository
* OrderRepository
* StorageRepository
* SupportRepository
5. Data Base
### Зовнішні інтеграції 
1. PaymentGateway
2. DeliveryService API
3. Email/Push
4. Google SSO service
## Порти
* HTTP in
* webhook in
* Delivery out
* Auth out
* Email/Push out
* PSP(payment service provider) out
## Залежності/Зв'язки
* Користувач ->(Пряма залежність) Web UI.
* WebUI -> порт HTTP in (lollipop  Rest API) -> Router.
* Від Router до усіх контролерів всередині пакеджу API(controllers) пунктирна лінія.
* Від AuthController -> AuthService -> User Repository. Через порт Auth out, lollipop зв'язок між AuthService і Google SSO.
* Від OrderController -> OrderService -> Order Repository. Також OrderService -> NotificationService.
* У NotificationService контракт lollipop з Email/Push через порт Email/Push out.
* У OrderService контракт lollipop з Delivery Service API через порт DeliveryData out.
* StorageController -> StorageService -> Storage Repository.
* PaymentController -> PromoService -> PaymentService і PaymentController -> PaymentService також PaymentMethodController -> PaymentService. PaymentService -> Payment Repository. 
* PaymentController зв'язок через порт PSP out з PaymentGateway. Тип lollipop. 
* PaymentGateway -> Webhook in(зв'язок Lollipop) -> PaymentWebhookController -> PaymentService.
* PaymentService -> NotificationService повідомляє про оплату чи невдачу.
* DeliveryServiceAPI -> webhook in -> PaymentWebhookController -> OrderService при отрманні посилки.
* Зв'язок від усіх репозиторіїв через порт SQLout до Бази даних, зв'язок lollipop.
* Користувач створює замовлення через WebUI -> Router -> SupportController -> SupportService -> SupportRepository.
* SupportService -> NotificationService -> Email/Push порт -> Менеджер підтримки отримує сповіщення.
* Менеджер підтримки відправляє відповідь -> WebUI -> Router -> SupportController -> SupportService -> SupportRepository. SuportService -> NotificationService відправлється відповідь користувачеві.