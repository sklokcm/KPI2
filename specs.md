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
6. ORDER
* order_id
* number
* status
* order_time
6. PAYMENT
* payment_id
* total_price
* status
* payment_time

## Зв'язки
* Користувач може створити від 0 до N замовлень
* Користувач може написати в підтримку від 0 до N разів
* Менеджер може оновлювати багато товарів
* Товар входить в багато категорій
* Категорія містить багато товарів 
* Користувач має рівно один кошик
* У кошику може знаходитись багато товарів
* У користувача може бути багато замовлень
* Замовлення може мати від 0 до N платежів(спроб)
* Платіж має зв'язок лише з одним замовленням


## Критерії
* Нормалізація 3NF
* Дозволяються зв'язки багато-до-багатьох
* За наявності власних атрибутів створюється власна сутність 