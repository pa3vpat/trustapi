# ViaBTC Saas API Observer

## 说明

协议：HTTPS

数据格式：JSON

Content-Type :'application/json'

路径：所有api以/res/saas开头

分页：page&limit参数，可选

二次验证：verify_type参数兼容google_code，sms/totp两种枚举类型，推荐使用前者。


## 目录

* [观察者](#观察者)
  * [观察者用户面板信息](#观察者用户面板信息)
  * [观察者算力曲线](#观察者算力曲线)
  * [观察者收益图表](#观察者收益图表)
  * [观察者收益记录](#观察者收益记录)
  * [观察者支付记录](#观察者支付记录)
  * [观察者信息](#观察者信息)
  * [观察者矿工分组列表](#观察者矿工分组列表)
  * [观察者矿工列表](#观察者矿工列表)
  * [观察者矿工算力曲线](#观察者矿工算力曲线)

-----

## 观察者

### 观察者用户面板信息

* 请求：

GET: /observer/home

|参数名|类型|必须|备注|
| -----|----|----|----|
| access_key | string | yes | 访问钥 |
| user_id | int | no | 主/子账户id，对于非全局观察者会忽略该参数，全局观察者时，不传则默认主账户id |
| coin | string | yes | 币种 |

* 响应：

```
{
  "code": 0,
  "data": {
    "account_balance": "0",
    "hash_unit": "TH/s",
    "hashrate_10min": "14.697T",    # 算力
    "hashrate_1day": "0.000",
    "hashrate_1hour": "2.449T",
    "profit_24hour": "0",           # 24小时收益
    "profit_total": "0.42526509",   # 总收益
    "target_24hour": "0.00002663",  # 单位算力每天预估收益
    "total_active": 2,              # 矿工数
    "total_unactive": 0
  },
  "message": "ok"
}
```

### 观察者算力曲线

* 请求：

GET: /observer/hashrate/chart

|参数名|类型|必须|备注|
| -----|----|----|----|
| access_key | string | yes | 访问钥 |
| user_id | int | no | 主/子账户id，对于非全局观察者会忽略该参数，全局观察者时，不传则默认主账户id |
| coin | string | yes | 矿池币种 |
| interval | string | yes | 间隔 （min、day、hour三种选择） |
| utc | string | no | true/false，当interval=day时有效。true: 以utc0点\~24点为一天，返回日维度的数据，false: 以北京时间0点\~24点为一天，返回日维度的数据。默认false |

* 响应：

```
{
  "code": 0,
  "data": {
    'start': 154248315,
    'unit': 'G',
    'hashrate': [14522,56451,25.15,1646.1,......],      
    'reject_rate': [22,24,25,......],   # 百分号前的数字     
  },
  "message": "ok"
}
```

### 观察者收益图表

* 请求：

GET: /observer/profit/chart

|参数名|类型|必须|备注|
| -----|----|----|----|
| access_key | string | yes | 访问钥 |
| user_id | int | no | 主/子账户id，对于非全局观察者会忽略该参数，全局观察者时，不传则默认主账户id |
| coin | string | yes | 币种 |
| utc | string | no | true/false |

* 响应：

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

### 观察者收益记录

分页

* 请求：

GET: /observer/profit/detail

|参数名|类型|必须|备注|
| -----|----|----|----|
| access_key | string | yes | 访问钥 |
| user_id | int | no | 主/子账户id，对于非全局观察者会忽略该参数，全局观察者时，不传则默认主账户id |
| coin | string | yes | 币种 |
| utc | string | no | true/false |

* 响应：

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
        "pps_plus_rate": "0.96",      # pps+收益比
        "pps_profit": "0.04379624",
        "solo_profit": "0",
        "total_profit": "0.04379624",
        "unit_output": "0.14595095"   # 单位收益
      }
    ],
    "has_next": false,
    "total": 8,
    "total_page": 1
  },
  "message": "ok"
}
```

### 观察者支付记录

分页

* 请求：

GET: /observer/payment/detail

|参数名|类型|必须|备注|
| -----|----|----|----|
| access_key | string | yes | 访问钥 |
| user_id | int | no | 主/子账户id，对于非全局观察者会忽略该参数，全局观察者时，不传则默认主账户id |
| coin | string | yes | 币种 |

* 响应：

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

### 观察者信息

* 请求：

GET: /observer/info

|参数名|类型|必须|备注|
| -----|----|----|----|
| access_key | string | yes | 访问钥 |
| user_id | int | no | 主/子账户id，对于非全局观察者会忽略该参数，全局观察者时，不传则默认主账户id |
| coin | string | no | 币种 |

* 响应：

```
{
  "code": 0,
  "data": {
    "account": "zhangsan",
    "global": true, # 是否全局观察者
    "accounts": [{  # global=true时返回，全局观察者的账户列表
      "user_id": 6,
      "account": "lisi"
    }],
    "coin": "BTC" # 不传币种时，后端返回有算力的第一个币种
  },
  "message": "ok"
}
```


### 观察者矿工分组列表

* 请求：

GET: /observer/worker/group

|参数名|类型|必须|备注|
| -----|----|----|----|
| access_key | string | yes | 访问钥 |
| coin | string | yes | 币种 |

* 响应：

```
{
  "code": 0,
  "data": [
    {
      "total": 0,   # 总矿工数
      "active": 0,  # 有效矿工数
      "group_id": -1,
      "group_name": "All Worker",  # 所有矿工
      "unactive": 0 # 无效矿工数
    },
    {
      "total": 0,   # 总矿工数
      "active": 0,  # 有效矿工数
      "group_id": 0,
      "group_name": "Default Group",  # 默认分组，无法修改删除
      "unactive": 0 # 无效矿工数
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

### 观察者矿工列表

分页

* 请求：

GET: /observer/worker

|参数名|类型|必须|备注|
| -----|----|----|----|
| access_key | string | yes | 访问钥 |
| user_id | int | no | 主/子账户id，对于非全局观察者会忽略该参数，全局观察者时，不传则默认主账户id |
| coin | string | yes | 币种 |
| group_id | int | yes | 分组id |
| worker_name | string | no | 矿工名 |
| status | string | no | active/unactive |
| sort_by | string | no | id/name/last_active/recent_hashrate |
| sort_order | string | no | asc/desc |

* 响应：

```
{
  "code": 0,
  "data": {
    "count": 1,
    "curr_page": 1,
    "data": [
      {
        "coin": "BCH",
        "group_id": 0,        # 分组id，默认分组为0
        "hashrate_10min": "0",  # 算力
        "hashrate_1day": "0",
        "hashrate_1hour": "0",
        "id": 470,
        "last_active": 1550802900,  # 最后激活时间
        "name": "1x2",    # 旷工名
        "recent_hashrate": "0", # 最近算力
        "status": "unactive", # 激活状态 active/unactive
        "user": "yangxing",  # 矿工所属用户名
        "reject_rate": "0"  # 拒绝率
      }
    ],
    "has_next": false,
    "total": 1,
    "total_page": 1
  },
  "message": "OK"
}
```

### 观察者矿工算力曲线

* 请求：

GET: /observer/worker/hashrate/chart

|参数名|类型|必须|备注|
| -----|----|----|----|
| access_key | string | yes | 访问钥 |
| user_id | int | no | 主/子账户id，对于非全局观察者会忽略该参数，全局观察者时，不传则默认主账户id |
| coin | string | yes | 币种 |
| worker_id | int | yes | 矿工id |
| interval | string | yes | min/hour/day |
| utc | string | no | true/false, 当interval=day时有效 |

* 响应：

```ying w
{
  "code": 0,
  "data": {
    "hashrate": [
      0.0,
      0.0
    ],
    "reject_rate": [
      0,
      0
    ],
    "start": 1545148800000,
    "unit": "G"
  },
  "message": "OK"

```
