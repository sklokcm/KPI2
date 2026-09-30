# Змінити зв'язки між MANAGER і PRODUCT та MANAGER і SUPPORT_MESSAGE 

## Context and Problem Statement
Зараз на діаграмі зв'язок між MANAGER та PRODUCT виглядає так ніби продукт може редагувати лише один менеджер. Схожа проблема у зв'язкові між MANAGER та SUPPORT_MESSAGE, де до запиту одразу підв'язаний менеджер, хоча коли запит тільки створений менеджер до нього ще не призначений.




## Decision Outcome
Зв'язок між MANAGER та PRODUCT багато до багатьох, змінити умову, що до SUPPORT_MESSAGE підріплений 0(ще не підкріплений) або 1 менеджер

