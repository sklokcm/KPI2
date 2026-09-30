## Сутності
1. USER
* user_id
* name
* password_hash
* phonenumber
* e-mail
* adress
* postcode
2. MANAGER
* manager_id
* name
* password_hash
3. PRODUCT
* product_id
* name
* description
* price
* stock_amount
4. CATEGORY
* category_id
* name
* description
5. CART
* cart_id
* total_price
6. CART_ITEM
* cart_id
* product_id
* quntity
7. ORDER
* order_id
* number
* status
* order_time
8. ORDER_ITEM
* order_id
* product_id
* quntity
* unit_price
9. PAYMENT
* payment_id
* total_price
* status
* payment_time
10. SUPPORT_MESSAGE
* message_id
* user_id
* manager_id
* message_text
* message_time 
* status


## Зв'язки
* Користувач може створити від 0 до N замовлень
* Користувач може написати в підтримку від 0 до N разів
* Менеджер може оновлювати багато товарів
* Товар входить в багато категорій
* Категорія містить багато товарів 
* Користувач має рівно один кошик
* У кошику може містится від 0 до N товарів кошику
* Продукт може бути товаром у кошику від 0 до N разів
* У замовленні може міститися від 0 до багатьох товарів 
* Замовлення може мати від 0 до N платежів(спроб)
* Платіж має зв'язок лише з одним замовленням
* Користувач може написати від 0 до N звернень, звернення підв'язане до одного користувача
* До звернення підкріплений 1 менеджер, менеджер може опрацьовувати багато звернень


## Критерії
* Нормалізація 3NF
* Дозволяються зв'язки багато-до-багатьох
* Тільки за наявності власних атрибутів створюється асоціативна сутність 