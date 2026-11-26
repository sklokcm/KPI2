## Prompt 

Було вирішено додати актора Менеджер підтримки, SupportController у шар API, SupportService у шар сервісів та SupportRepository у шар доступу до даних.
- Користувач створює замовлення через WebUI -> Router -> SupportController -> SupportService -> SupportRepository.
- SupportService -> NotificationService -> Email/Push порт -> Менеджер підтримки отримує сповіщення.
- Менеджер підтримки відправляє відповідь -> WebUI -> Router -> SupportController -> SupportService -> SupportRepository. SuportService -> NotificationService відправлється відповідь користувачеві.

Додай описані компоненти та зв'язки у діаграму 

## AI response
Оновлений код PlantUML із доданим актором Менеджер підтримки, компонентами SupportController, SupportService, SupportRepository та всіма описаними залежностями:

Що додано:
Актор та UI: Додано актора Менеджер підтримки (SupportManager) зі зв'язком до Web UI (для відправки відповідей через WebUI -> Router -> SupportController).

Шари системи: Додано SupportController у шар API (controllers), SupportService у шар Services та SupportRepository у шар Data Access (Repositories) із пунктирними стрілками залежностей.

Потік сповіщень: Додано залежність SupportService .right.> NotificationService, а також зв'язки від зовнішнього Email/Push до акторів Менеджер підтримки та Користувач для доставки сповіщень про звернення та відповідь.

Робота з БД: Додано суцільну стрілку від SupportRepository до порту SQL out.