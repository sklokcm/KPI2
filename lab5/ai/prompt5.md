## Prompt 

Було вирішено додати актора Менеджер підтримки, SupportController у шар API, SupportService у шар сервісів та SupportRepository у шар доступу до даних.
- Користувач створює замовлення через WebUI -> Router -> SupportController -> SupportService -> SupportRepository.
- SupportService -> NotificationService -> Email/Push порт -> Менеджер підтримки отримує сповіщення.
- Менеджер підтримки відправляє відповідь -> WebUI -> Router -> SupportController -> SupportService -> SupportRepository. SuportService -> NotificationService відправлється відповідь користувачеві.

Додай описані компоненти та зв'язки у діаграму 

## AI response
Оновлений код PlantUML із доданим вхідним портом Webhook in, контрактом Webhook API, компонентами PaymentWebhookController та PaymentWebhookService, а також усіма новими зв'язками для обробки колбеків від PaymentGateway та DeliveryService API:

Що додано та оновлено:
Вхідний порт та контракт: Додано portin "Webhook in" на межу Backend та інтерфейс-контракт Webhook API (lollipop), до якого підключені PaymentGateway та DeliveryService API.

Нові компоненти: До шару API (controllers) додано PaymentWebhookController (приймає запити безпосередньо з Webhook in, оминаючи Router), а до шару Services — PaymentWebhookService.

Нові залежності в шарах:

PaymentWebhookController .down.> PaymentWebhookService

PaymentWebhookService .left.> PaymentService (для обробки колбеків оплати)

PaymentWebhookService .right.> OrderService (для обробки підтверджень доставки посилки)

PaymentService .right.> NotificationService (для відправки повідомлень про успішну або невдалу оплату).

## Prompt 
PaymentWebhookService не має бути

## AI response
Оновлений код PlantUML без PaymentWebhookService — тепер PaymentWebhookController звертається напряму до PaymentService та OrderService: