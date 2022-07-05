# Описание API топливного кабинета

## Получение транзакционного отчета 
### URL: **/api/gettransaction/**

POST - запрос

**Content-type:application/x-www-form-urlencoded**

Параметры передаются в теле запроса (все параметры являются обязательными): 
- username - имя пользователя личного кабинета 
- password - пароль пользователя личного кабинета 
- startDate -  дата начала транзакционного отчета в формате (YYYY-MM-DD)
- endDate -  дата окончания транзакционного отчета в формате (YYYY-MM-DD)
- type - формат ответа (XLS или JSON)

---
## Получение оперативного отчета 
### URL: **/api/getoperdata**

POST - запрос

**Content-type:application/x-www-form-urlencoded**

Параметры передаются в теле запроса (все параметры являются обязательными): 
- username - имя пользователя личного кабинета 
- password - пароль пользователя личного кабинета 
- startDate -  дата начала транзакционного отчета в формате (YYYY-MM-DD)
- endDate -  дата окончания транзакционного отчета в формате (YYYY-MM-DD)

Не обязательный параметр: 
- cardNumber  - отбор по номеру карты

Ответ для данного запроса (в формате XLS)

---
## Получение отчета по лимитам 
### URL: **/api/getlimitdata**

POST - запрос

**Content-type:application/x-www-form-urlencoded**

Параметры передаются в теле запроса (все параметры являются обязательными): 
- username - имя пользователя личного кабинета * password - пароль пользователя личного кабинета 
- startDate -  дата начала транзакционного отчета в формате (YYYY-MM-DD)
- endDate -  дата окончания транзакционного отчета в формате (YYYY-MM-DD)

Не обязательный параметр: 
- cardNumber  - отбор по номеру карты

Ответ для данного запроса (в формате XLS)

---
## Получение баланса
### URL: **/api/getbalance**

POST - запрос

**Content-type:application/x-www-form-urlencoded**

Параметры передаются в теле запроса (все параметры являются обязательными): 
username - имя пользователя личного кабинета 
password - пароль пользователя личного кабинета 

Ответ для данного запроса (в формате JSON):

    {
        "opening_balance": "-209723.06", - Остаток на начало месяца
        "incoming": "6543000.00", - Поступление на счет
        "expence": "0.00", - Расход
        "g_abalcncee": "0.00", - Баланс электронного кошелька
        "available": 1201523.51, - Остаток
        "free": 1201523.51 - Свободные средства к распределению по ЭК
    }

---
## Получение списка платежей
### URL: **/api/paymentdata**

POST - запрос

**Content-type:application/x-www-form-urlencoded**

Параметры передаются в теле запроса (все параметры являются обязательными): 
- username - имя пользователя личного кабинета 
- password - пароль пользователя личного кабинета 
- startDate -  дата начала транзакционного отчета в формате (YYYY-MM-DD)
- endDate -  дата окончания транзакционного отчета в формате (YYYY-MM-DD)

Ответ для данного запроса (в формате JSON):

    [
        {
            "period": "2018-03-22",
            "sum": "198000.00",
            "income_number": "6525",
            "payment_details": "за топливо по Дог.NСМ15/000263/ЛК10 от 23,10,15 по счету N78 от 16,03,18 Cумма 198000-00,в т.ч. НДС(18%) - 30203-39.",
            "contracts_id": "f65b4e7b-830c-11e5-92ca-0017317d4c20"
        },
        {
            "period": "2018-03-22",
            "sum": "198000.00",
            "income_number": "6525",
            "payment_details": "за топливо по Дог.NСМ15/000263/ЛК10 от 23,10,15 по счету N78 от 16,03,18 Cумма 198000-00,в т.ч. НДС(18%) - 30203-39.",
            "contracts_id": "f65b4e7b-830c-11e5-92ca-0017317d4c20"
        }
    ]

___
## Изменение лимита топливной карты
### URL: **/api/editlimit**

**Content-type:application/x-www-form-urlencoded**

Параметры передаются в теле запроса (все параметры являются обязательными): 
- username - имя пользователя личного кабинета 
- password - пароль пользователя личного кабинета 
- data - строка в формате json содежащая параметры изменения лимита.

Описание параметра **data.

| Параметр     |     Тип       |     Описание |
------------- | ------------- | ------------
card_number  | string | Номер топливной карты 
limits 		 | [string] | Лимиты для изменения
productType | string | Код вида топлива
limit_value| string | Значение лимита
limit_unit_code | string | Изменение лимита
limit_period_code | string | Период действия лимита

Пример параметра **data

    {
       "card_number": "7820000000000001061",
       "limit_schema": "LPCT",
       "limit_type_code": "INDIVID",
       "limits": [
         {
           "productType": "00013",
           "limit_value": "450",
           "limit_unit_code": "L",
           "limit_period_code": "MONTH"
         },
         {
           "productType": "00014",
           "limit_value": "1000",
           "limit_unit_code": "RU",
           "limit_period_code": "DAY"
         }
       ]
     }

 Справочники
---
**Виды топлива**
| Код | Наименование |
|---- | ---------- |
|00013|  Дизельное топливо
|00014|  Регуляр-92
|00015|  Премиум-95
|00064|  СУГ / Метан
|00073|  Супер-98 / ЭКТО 100
|00081|  Премиум-95 ЭКТО
---
**Изменение лимита**
| Код | Наименование |
| -- | ----- |
| L  | Литры |
| RU | Рубли |
---
**Период действия лимита**
| Код | Наименование |
|--|--|
| DAY  | Суточный |
| WEEK  | Недельный |
| MONTH  | Месячный |
| QUARTER  | Квартальный |
| HALFYEAR  | Полугодовой |
| YEAR  | Годовой |
---

## Изменение статуса топливной карты
### URL: **/api/ulockcard**

**Content-type:application/x-www-form-urlencoded**

Параметры передаются в теле запроса (все параметры являются обязательными): 
- username - имя пользователя личного кабинета 
- password - пароль пользователя личного кабинета 

В теле запроса необходимо передать данные в формате JSON.
Описание параметров тела запроса.
| Параметр     |     Тип       |     Описание |
------------- | ------------- | ------------
card_number  | string | Номер топливной карты 
status 		 | string | Новый статус карты 

    {
       "card_number": "7820000000000001061",
       "status": "unlock",
     }
 Справочники
---
**Статус карты**
| Код | Наименование |
|---- | ---------- |
|lock|  Заблокирована
|unlock|  В работе

