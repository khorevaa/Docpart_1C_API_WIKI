# Общие параметры


Для всех запросов обязательна передача заголовка

'content-type: application/x-www-form-urlencoded'

В параметрах POST-запроса есть два общих для всех методов параметра:
- task – Тип: Строка - имя метода API для выполнения
- tech_key – Тип: Строка - Ключ для вызова скриптов. Его необходимо взять из панели управления платформы Docpart в разделе «Настройки».

При вызове любого метода будет возвращена JSON-структура с полями:

- status – Тип: Булево – статус выполнения метода
- message – Тип: Строка – Сообщение об ошибке
- data – Тип: Структура - Результат выполнения метода

## Проверка соединения с сервисом
Метод используется для проверки связи с сайтом и корректности указания настроек обмена.

Операция: check_connection

Параметры запроса:

|Параметр | Пример заполнения |	Описание|
|---|---|---|
|tech_key *|TEST_KEY_FROM_SETTINGS|Тип: Строка – Ключ для вызова скриптов|

При успешном выполнении метод возвращает стурктуру JSON с полями:

Поле	Тип значения	Описание
status	Булево	статус выполнения метода
message	Строка	всегда возвращает текст «ОК»


Получение списка состояний заказов
==================================

Получение списка возможных состояний заказов и позиций заказов

Операция: **get_statuses_description**

Параметры запроса:

| **Параметр** | **Пример заполнения** | **Описание**
|---|---|---|
| tech_key *| TEST_KEY_FROM_SETTINGS | Строка – Ключ для вызова скриптов|
| orders |1|Булево, Если Истина, то в результат будет добавлен список состояний заказов|
|order\_items|1|Булево, Если Истина, то в результат будет добавлен список состояний позиций заказов (товаров)|

В результате выполнения метода будет возвращена JSON-структура с полями:

|**Поле**|**Описание**|
|---|---|
|status| Булево – статус выполнения метода|
|message|Строка – всегда возвращает текст «ОК»|
|data|Запрашиваемые данные|При успешном выполнении метод возвращает данные \[data\]:|


|**Поле**|**Описание**|
|---|---|
|orders|Массив состояний заказа|
|order\_items| Массив состояний позиций заказа (товаров)|


Структура массива состояний заказов - orders:

|**Поле**|**Описание**|
|---|---|
|id|Число, Идентификатор статуса|
|name|Строка, Наименование статуса|
|color|Строка, Цвет статуса на сайте|
|for\_paid|Булево, Статус устанавливается для оплаченных заказов|
|for\_created|Булево, статус устанавливается для новых заказов|
|order|Число, порядок сортировки|

Структура массива состояний заказов - order\_items:

|**Поле**|**Описание**|
|---|---|
|id|Число, Идентификатор статуса позиции|
|name|Строка, Наименование статуса позиции|
|color|Строка, Цвет статуса позиции на сайте|
|count\_flag|Булево, при установке статуса товар с наличия будет зарезервирован|
|issue\_flag|Булево, при устанвоке статуса товар будет выдан покупателю|
|for\_created|Булево, статус устанавливается для новых заказов|
|order|Число, порядок сортировки|