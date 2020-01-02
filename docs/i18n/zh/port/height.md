# 体高

* [请求数据](#请求数据)
* [提交数据](#提交数据)


## 请求数据

请求方法 GET

|参数名称|必须|数据类型|示例数据|描述|
|-|:-:|:-:|:-|:-|
|tstart|否|timestamp|1562150930000|开始时间（秒）|
|tend|否|timestamp|1562150939000|截止时间（秒）|
|oid|否|bigint|10003|被测对象编号|
|height|否|smallint|300152|体高（mm）|
|did|否|bigint|1001|设备编号|
|limit|否|正整数|1000|行数|

注意：
* etime > stime ,区间 (stime,etime]
* limit 不传，默认 1000

示例：

```
height?stime=1562150930000&oid=10003&limit=100
```

等价于：

```sql
select time, oid, height, did from height where stime > 1562150930000 and oid = 10003 limit 100
```

### 2、响应

|参数名称|必须|数据类型|描述|
|-|:-:|:-:|:-|
|code|是|int|返回码|
|msg|是|string|返回信息|
|+data|是|array|结果集|
|+fields|是|array|结果集对应字段|

示例：
```json
{
    "code": 0,
    "msg": "ok",
    "data": [
        [
            "2019-10-02T01:11:29.356Z",
            "1n",
            1000,
            "1n"
        ],
        [
            "2018-06-01T04:38:03.001Z",
            "10003n",
            15387,
            "1001n"
        ]
    ],
    "fields": [
        "ts",
        "oid",
        "height",
        "did"
    ]
}
```

## 提交数据

### 1、请求

请求方法 POST

content-type：text/plain

|参数名称|必须|数据类型|示例数据|描述|
|-|:-:|:-:|:-|:-|
|time|是|timestamp|1562150939000|时间戳（秒）|
|oid|是|bigint|10003|被测对象编号|
|height|是|smallint|15387|体高（mm）|
|did|是|bigint|1001|设备编号|

注意：
* time 不能是 0

示例：
```json
{
    "did": 1001,
    "data": [{
            "time": "1527827986002",
            "oid": "10002n",
            "height": 15387,
        },
        {
            "time": "1527827987004",
            "oid": "10001n",
            "height": 17387,
        }
    ]
}
```

### 2、响应

|参数名称|必须|数据类型|描述|
|-|:-:|:-:|:-|
|code|是|int|返回码|
|msg|是|string|返回信息|
|data|是|object|一般是空|

示例：

```json
{
    "code": 0,
    "msg": "ok"
}
```
