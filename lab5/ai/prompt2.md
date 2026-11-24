## Prompt 
Generate syntaxys for UML diagram, pay attention to all the criteria, do not make any changes yet.

## AI response
Ось опис структури та PlantUML-код для діаграми компонентів, що повністю відповідає вашим критеріям (горизонтальні шари, порти, контракти lollipop, правильний напрямок зв'язків та застереження щодо відсутності залежностей вгору).

Короткі коментарі до структури:
Шари (Layers): Відділено Web UI, API (Controllers), Services, Data Access (Repositories) та Database за допомогою пакетів (як горизонтальні шари, що йдуть стопкою зверху вниз).

Зв'язки: Внутрішні залежності всередині шарів/суміжних шарів (Controller -> Service -> Repository) позначені як пунктирні стрілки (.down.>). Зовнішні інтеграції та виклики портів — суцільними лініями.

Порти (lollipop): Створено порти: HTTP in на вході в систему; Auth out, Delivery out, Email/Push out, PSP out на межах зовнішніх інтеграцій; а також спільний SQL out інтерфейс на підключення до Бази даних (DB).

Зовнішні системи: Google SSO, Delivery API, Notification Gateway та Payment Gateway розміщені за межами ноди System у вигляді окремих, не об'єднаних пакетів, щоб відповідати Use Case.