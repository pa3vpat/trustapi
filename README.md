# Api для Trustpool.ru

## Описание

Тип запроса：HTTPS

Формат：JSON

Content-Type :'application/json'

Путь：trustpool.ru/res/saas/

## Оглавление



-----
## Вотчер / Watcher / Наблюдатель

### Главная страница
* get запрос: trustpool.ru/res/saas/observer/home?

|Параметр|Тип данных|Обязательный?|Комментарий|
| -----|----|----|----|
| access_key | string | yes | Ключ доступа,  trustpool.ru/setting/observer, тут можно получить.|
| user_id | int | no | Идентификатор пользователя |
| coin | string | yes | Валюта BTC/ETH  и тд |

Пример: trustpool.ru/res/saas/observer/home?access_key=ВАШ_access_key&coin=BTC

Вернет:
```
{
  "code": 0,
  "data": {
    "account_balance": "0",
    "hash_unit": "TH/s",
    "hashrate_10min": "14.697T",    
    "hashrate_1day": "0.000",
    "hashrate_1hour": "2.449T",
    "profit_24hour": "0",           
    "profit_total": "0.42526509",  
    "target_24hour": "0.00002663",  
    "total_active": 2,              
    "total_unactive": 0
  },
  "message": "ok"
}
```

### График хешрейта
* get запрос: trustpool.ru/res/saas//observer/hashrate/chart
|Параметр|Тип данных|Обязательный?|Комментарий|
| -----|----|----|----|
| access_key | string | yes | Ключ доступа,  trustpool.ru/setting/observer, тут можно получить.|
| user_id | int | no | Идентификатор пользователя |
| coin | string | yes | Валюта BTC/ETH  и тд |
| interval | string | yes | Принимает параметры: min, hour, day|
| utc | string | no |  Принимает: true или false. True - вернет данные по UTC времени. False - по пекинскому времени|

Пример: trustpool.ru/res/saas/observer/hashrate/chart?access_key=ACCES_KEY&coin=BTC&interval=day&utc=true

* Вернет：

```
{
  "code": 0,
  "data": {
    'start': 154248315,
    'unit': 'T',
    'hashrate': [14522,56451,25.15,1646.1,......],      
    'reject_rate': [22,24,25,......],        
  },
  "message": "ok"
}
```

### График доходов

* get запрос:  trustpool.ru/res/saas/observer/profit/chart?

|Параметр|Тип данных|Обязательный?|Комментарий|
| -----|----|----|----|
| access_key | string | yes | Ключ доступа,  trustpool.ru/setting/observer, тут можно получить.|
| user_id | int | no | Идентификатор пользователя |
| coin | string | yes | Валюта BTC/ETH  и тд |
| utc | string | no |  Принимает: true или false. True - вернет данные по UTC времени. False - по пекинскому времени|

Пример:trustpool.ru/res/saas/observer/profit/chart?access_key=ACCESS_KEY&coin=BTC&utc=true

* Вернет：

```
{
  "code": 0,
  "data": {
    'start': 154248315,
    'profit': [14522,56451,25.15,1646.1,......],
  },
  "message": "ok"
}
```


### Детальная информация о доходах

GET: trustpool.ru/res/saas/observer/profit/detail?

|Параметр|Тип данных|Обязательный?|Комментарий|
| -----|----|----|----|
| access_key | string | yes | Ключ доступа,  trustpool.ru/setting/observer, тут можно получить.|
| user_id | int | no | Идентификатор пользователя |
| coin | string | yes | Валюта BTC/ETH  и тд |
| utc | string | no |  Принимает: true или false. True - вернет данные по UTC времени. False - по пекинскому времени|

* Вернет：
```
{
  "code": 0,
  "data": {
    "count": 8,
    "curr_page": 1,
    "data": [
      {
        "coin": "BTC",
        "date": "2019-06-28",
        "hash_unit": "TH/s",
        "hashrate": "30023636346.00",
        "pplns_profit": "0",
        "pps_plus_rate": "0.96",      
        "pps_profit": "0.04379624",
        "solo_profit": "0",
        "total_profit": "0.04379624",
        "unit_output": "0.14595095"   
      }
    ],
    "has_next": false,
    "total": 8,
    "total_page": 1
  },
  "message": "ok"
}
```

### Детальная информация о выплатах

* get запрос:  trustpool.ru/res/saas/observer/payment/detail?

|Параметр|Тип данных|Обязательный?|Комментарий|
| -----|----|----|----|
| access_key | string | yes | Ключ доступа,  trustpool.ru/setting/observer, тут можно получить.|
| user_id | int | no | Идентификатор пользователя |
| coin | string | yes | Валюта BTC/ETH  и тд |
| utc | string | no |  Принимает: true или false. True - вернет данные по UTC времени. False - по пекинскому времени|

* Вернет：

```
{
  "code": 0,
  "data": {
    "count": 4,
    "curr_page": 1,
    "data": [
      {
        "address": "3MbMG4usCx7K9PGQCcY2NrXTZoK5hYNgKF",
        "address_url": "https://explorer.viawallet.com/btc/address/3MbMG4usCx7K9PGQCcY2NrXTZoK5hYNgKF",
        "amount": "0.0750074",
        "coin": "BTC",
        "status": "completed",
        "time": 1550823507,
        "tx_url": "https://explorer.viawallet.com/btc/tx/33faaeb8f4880572cc55cb6305e66f281b79341a6cb3e4cea9b6e598db981aa7",
        "txid": 33faaeb8f4880572cc55cb6305e66f281b79341a6cb3e4cea9b6e598db981aa7
      }
    ],
    "has_next": false,
    "total": 4,
    "total_page": 1
  },
  "message": "OK"
}
```

### Информация о Вотчере

* get запрос: trustpool.ru/res/saas/observer/info?

|Параметр|Тип данных|Обязательный?|Комментарий|
| -----|----|----|----|
| access_key | string | yes | Ключ доступа,  trustpool.ru/setting/observer, тут можно получить.|
| user_id | int | no | Идентификатор пользователя |
| coin | string | no | Валюта BTC/ETH  и тд |

* Вернет：

```
{
  "code": 0,
  "data": {
    "account": "pa3vpat",
    "global": true, 
    "accounts": [{  
      "user_id": 6,
      "account": "lisi"
    }],
    "coin": "BTC"
  },
  "message": "ok"
}
```

### Информация о группах устройств

(trustpool.ru/pool/worker там слева "мои группы")

* get запрос: trustpool.ru/observer/worker/group?

|Параметр|Тип данных|Обязательный?|Комментарий|
| -----|----|----|----|
| access_key | string | yes | Ключ доступа,  trustpool.ru/setting/observer, тут можно получить.|
| coin | string | no | Валюта BTC/ETH  и тд |

* Вернет：

```
{
  "code": 0,
  "data": [
    {
      "total": 0,   
      "active": 0,  
      "group_id": -1,
      "group_name": "All Worker", 
      "unactive": 0 
    },
    {
      "total": 0,  
      "active": 0, 
      "group_id": 0,
      "group_name": "Default Group",  
      "unactive": 0 
    },
    {
      "total": 0,
      "active": 0,
      "group_id": 14,
      "group_name": "\u4e8c\u53f7\u6539\u516b\u578b\u5206\u961f",
      "unactive": 0
    }
  ],
  "message": "OK"
}
```

### Информация о воркерах

* get запрос: trustpool.ru/observer/worker?

|Параметр|Тип данных|Обязательный?|Комментарий|
| -----|----|----|----|
| access_key | string | yes | Ключ доступа,  trustpool.ru/setting/observer, тут можно получить.|
| coin | string | no | Валюта BTC/ETH  и тд |
| user_id | int | no | Идентификатор пользователя |
| group_id | int | yes | Ид группы устройств (узнавать через * [Тут](#Информация о группах устройств)) |
| worker_name | string | no | 矿工名 |
| status | string | no | active/unactive |
| sort_by | string | no | id/name/last_active/recent_hashrate |
| sort_order | string | no | asc/desc |
