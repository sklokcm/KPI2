## Prompt 
Порти повинні бути описані через portin i portout

## AI response
Оновлений код PlantUML із використанням ключових слів portin та portout, а також урахуванням усіх попередніх вимог до структури шарів, межі Backend, окремого розміщення зовнішніх інтеграцій і типів стрілок:

Що змінено:
portin / portout: Порт HTTP in оголошено через portin, а всі вихідні порти (Auth out, Email/Push out, Delivery out, PSP out, SQL out) — через portout безпосередньо на межі пакета Backend.

Межі та пакування: Пакети API (controllers), Services та Data Access (Repositories) об'єднані в пакет Backend, а Web UI і Data Base розміщені на рівні System поза Backend. Зовнішні сервіси винесені за межі System як окремі компоненти без спільного пакета.