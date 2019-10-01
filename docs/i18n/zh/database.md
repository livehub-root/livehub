# 数据库相关


## livehub

```sql
$ CREATE DATABASE IF NOT EXISTS livehub
```

### 建表

记录设备生产的数据，设备编号、被测实体编号为元数据，测量数据为数据

* did：device id，bigint
* oid：object id，bigint

表名称

* height：身高
* weight：牛


#### height

|字段|类型|说明|
|-|-|-|
|time|timestamp|时间主键|
|height|smallint|体高|
|did|bigint|设备编号|
|oid|bigint|牛编号|

**体高单位：毫米（mm）**

建超级表

```sql
$ CREATE TABLE livehub.height (ts timestamp, height smallint) TAGS(did bigint, oid bigint)
```

添加

```sql
$ CREATE TABLE h2_2 USING livehub.height TAGS (2, 2)
```

自动创建字表

```sql
$ INSERT INTO h1_1 USING livehub.height TAGS (1, 1) VALUES (0, 1000)
```


删除

```sql
$ DROP TABLE h2_2
```

#### weight

|字段|类型|说明|
|-|-|-|
|time|timestamp|时间主键|
|weight|int|体重|
|did|bigint|设备编号|
|oid|bigint|牛编号|

**体重单位：克（g）**


建超级表

```sql
$ CREATE TABLE livehub.weight (ts timestamp, height int) TAGS(did bigint, oid bigint)
```

添加

```sql
$ CREATE TABLE w2_2 USING livehub.weight TAGS (2, 2)
```

自动创建字表

```sql
$ INSERT INTO w1_1 USING livehub.weight TAGS (1, 1) VALUES (0, 1000)
```


删除

```sql
$ DROP TABLE w2_2
```