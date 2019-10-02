# 数据库相关


## livehub

```sql
$ CREATE DATABASE IF NOT EXISTS livehub
```

### 建表

记录设备生产的数据，设备编号、被测实体编号为元数据，测量数据为数据

* did：device id，bigint
* oid：object id，bigint

注意：为了数据整顿，did 为标签，oid 为数据。

表名称

* height：身高
* weight：牛


#### height

|字段|类型|说明|
|-|-|-|
|time|timestamp|时间主键|
|oid|bigint|牛编号|
|height|smallint|体高|
|did|bigint|设备编号|

**体高单位：毫米（mm）**

建超级表

```sql
$ CREATE TABLE livehub.height (ts timestamp, oid bigint, height smallint) TAGS(did bigint)
```

添加

```sql
$ CREATE TABLE height2 USING livehub.height TAGS (2)
```

自动创建字表

```sql
$ INSERT INTO height1 USING livehub.height TAGS (1) VALUES (0, 1, 1000)
```


删除

```sql
$ DROP TABLE height2
```

#### weight

|字段|类型|说明|
|-|-|-|
|time|timestamp|时间主键|
|oid|bigint|牛编号|
|weight|int|体重|
|did|bigint|设备编号|

**体重单位：克（g）**


建超级表

```sql
$ CREATE TABLE livehub.weight (ts timestamp, oid bigint, weight int) TAGS(did bigint)
```

添加

```sql
$ CREATE TABLE weight2 USING livehub.weight TAGS (2)
```

自动创建字表

```sql
$ INSERT INTO weight1 USING livehub.weight TAGS (1) VALUES (0, 1, 1000)
```


删除

```sql
$ DROP TABLE weight2
```