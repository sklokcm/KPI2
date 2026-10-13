## Prompt
Read specs.md and give a feedback on what can be added or changed about requirements.

## AI response
The current specification is understandable and captures a few important flows, but it still needs more precision and completeness to be a solid requirements document.

What works well
The list of actors is clear enough.
The functional requirements already cover the main business scenarios: authentication, support queue, stock validation, and payment failure.
The non-functional section includes a basic security and performance expectation.
What should be improved
1. Requirements are too general and not fully testable
Several statements are vague:

“інтуїтивний користувацький інтерфейс” — what does “intuitive” mean in practice?
“опрацьовувати кожну операцію за 3с” — does this mean average response, 95th percentile, or maximum time?
“Google SSO” — is account linking required, and what happens when an email already exists?
A requirement should be measurable. For example:

“95% of API requests must complete within 3 seconds under 2000 concurrent users.”
“The system must provide responsive UI for desktop and mobile screens with a minimum 320px width.”
“Users may sign in with email/password or Google account, and an existing email must be linked to the same account without duplication.”
2. Missing important user flows
The document currently focuses only on a few cases, but the system likely needs more requirements:

registration and account creation
password recovery / reset
log out / session expiration
adding/removing items from cart
updating cart quantities
placing an order
payment retries / timeouts
order cancellation and refund
delivery status tracking
support ticket status lifecycle
3. Need clearer status and business rules
The support and payment requirements should define exact state transitions:

support ticket states: open → in progress → resolved → closed.
payment states: pending → success → failed → refunded.
order states: created → paid → confirmed → shipped → delivered → canceled.
Right now, it is not always clear who changes the status and what triggers it.

4. Requirements should be written in a consistent template
A more formal style would make them easier to validate:

Actor
Action
Condition
Result
Example:

“When a user attempts to place an order and any cart item is out of stock, the system must block order submission and show a clear notification.”
“When a payment is not confirmed within 30 seconds, the system must mark the payment as failed, cancel the order, and release the reserved stock.”
5. Non-functional requirements need specific metrics
The current NFRs are too weak:

“Шифрувати паролі” should specify hashing algorithm, for example bcrypt or Argon2.
“Інтуїтивний інтерфейс” should include accessibility or usability expectations.
“3 seconds under 2000 users” should specify the exact operation and percentile.
Recommended improvement:

“The system must hash user passwords using Argon2 or bcrypt.”
“The system must support 2000 concurrent users with 95% of requests under 3 seconds.”
“The UI must support keyboard navigation and meet basic WCAG accessibility requirements.”
Suggested additions to the document
I would add sections like:

User registration and login
Cart and checkout
Payment and order processing
Support service flow
Delivery and tracking
Security and privacy
Error handling and rollback rules
Example of stronger wording
“Користувач може зареєструватися за допомогою email/password або через Google SSO. Якщо email уже використовується, система має показати повідомлення та запропонувати вхід або відновлення доступу.”
“Якщо в кошику є товари, яких немає в наявності, система забороняє оформлення замовлення і виділяє ці товари в інтерфейсі.”
“Якщо платіжний сервіс не підтверджує оплату протягом 30 секунд, система встановлює статус платежу failed, скасовує замовлення і повертає товари на склад.”
Final verdict
The spec has a good starting structure, but it should be made more formal, measurable, and complete. The biggest improvements are:

add missing business flows,
define states and transitions,
make NFRs measurable,
rewrite requirements in a consistent, testable format.