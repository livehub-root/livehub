# 体重


## 请求数据

请求方法 GET

|参数名称|必须|数据类型|示例数据|描述|
|-|:-:|:-:|:-|:-|
|stime|否|timestamp|1562150930000|开始时间（秒）|
|etime|否|timestamp|1562150939000|截止时间（秒）|
|oid|否|bigint|10003|被测对象编号|
|weight|否|int|300152|体重（g）|
|did|否|bigint|1001|设备编号|
|limit|否|正整数|1000|行数|

注意：
* etime > stime ,区间 (stime,etime]
* limit 不传，默认 1000

示例：

```
weight?stime=1562150930000&oid=10003&limit=100
```

等价于：

```sql
select time, oid, weight, did from weight where stime > 1562150930000 and oid = 10003 limit 100
```

### 2、响应

|参数名称|必须|数据类型|描述|
|-|:-:|:-:|:-|
|code|是|int|返回码|
|msg|是|string|返回信息|
|data|是|object|结果集|

示例：
```json
{
    "code": 0,
    "msg": "ok",
    "data": [
        {
            "time": "2018-06-01 12:38:03",
            "oid": 10003,
            "weight": 15387,
        },
        {
            "time": "1527827884001",
            "oid": 10004,
            "weight": 17387,
        }
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
|weight|是|smallint|300152|体重（g）|
|did|是|bigint|1001|设备编号|

注意：
* time 不能是 0

示例：
```json
{
    "did": 1001,
    "data": [
        {
            "time": "2018-06-01 12:38:03",
            "oid": 10003,
            "weight": 15387,
        },
        {
            "time": "1527827884001",
            "oid": 10004,
            "weight": 17387,
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
    "msg": "ok",
    "data": {}
}
```
