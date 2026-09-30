## Сутності
1. USER
* user_id
* name
* password_hash
* phone_number
* email
2. ADDRESS
* address_id
* user_id
* city
* street
* building
* post_code
3. MANAGER
* manager_id
* name
* password_hash
4. PRODUCT
* product_id
* name
* description
* price
* stock_amount
5. CATEGORY
* category_id
* name
* description
6. CART
* cart_id
* user_id
7. CART_ITEM
* cart_id
* product_id
* quntity
8. ORDER
* order_id
* user_id
* address_id
* number
* status
* order_time
9. ORDER_ITEM
* order_id
* product_id
* quntity
* unit_price
10. PAYMENT
* payment_id
* total_price
* status
* payment_time
11. SUPPORT_MESSAGE
* message_id
* user_id
* manager_id
* message_text
* message_time 
* status


## Зв'язки
* Користувач може створити від 0 до N замовлень
* У користувача може бути багато адрес, кожна адреса відноситься до одного користувача
* Користувач може написати в підтримку від 0 до N разів
* Менеджер може оновлювати багато товарів
* Товар мають право редагувати багато менеджерів
* Товар входить в багато категорій
* Категорія містить багато товарів 
* Користувач має рівно один кошик
* У кошику може містится від 0 до N товарів кошику
* Продукт може бути товаром у кошику від 0 до N разів
* У замовленні може міститися від 0 до багатьох товарів 
* Замовлення може мати від 0 до N платежів(спроб)
* Замовлення приходить на одну адресу, а на одну адресу може прийти від нуля до багато замовлень
* Платіж має зв'язок лише з одним замовленням
* Користувач може написати від 0 до N звернень, звернення підв'язане до одного користувача
* До звернення підкріплений 1 менеджер(0 якщо жоден менеджер ще не відповів на запит), менеджер може опрацьовувати багато звернень


## Критерії
* Нормалізація 3NF
* Дозволяються зв'язки багато-до-багатьох
* Тільки за наявності власних атрибутів створюється асоціативна сутність 