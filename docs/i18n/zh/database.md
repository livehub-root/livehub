# 数据库相关

数据表命名
* 实体用英文复数
* 数据表用名词+动词方式

## livehub_user

基于 RBAC 设计的用户权限访问控制：用户、角色和权限

* [无组设计参考](https://shuwoom.com/?p=3041)
* [带组设计参考](https://blog.csdn.net/ljw499356212/article/details/81055141)

本设计为无组

### 建表

实体表

* users：用户
* roles：角色
* permissions：权限

关系表
* user_role：用户角色对照
* role_permission：角色权限对照

#### users

|字段|类型|说明|
|-|-|-|
|time|TIMESTAMP|时间主键|
|uid|binary(32)|md5(name)|

## livehub

livehub：设备与数据相关库，存放设备信息和设备生产的数据、辅助记录信息

```sql
$ CREATE DATABASE IF NOT EXISTS livehub
```

### 建表

实体表

* meadows：牧场
* cattles：牛
* cattle_scales：牛秤

数据表

* cattle_scale_measure：牛秤测量数据



#### meadows

#### cattles

|字段|类型|说明|
|-|-|-|
|time|TIMESTAMP|时间主键|
|cid|bigint|编号|


#### cattle_scales

#### cattle_scale_measure


