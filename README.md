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
* get запрос:

trustpool.ru/res/saas/observer/home?

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
