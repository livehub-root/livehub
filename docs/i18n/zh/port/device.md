# 设备管理

设备注册流程：
- 管理员添加设备信息，添加包括设备序列号SN和注册码；
- 设备访问注册接口，传入设备编号SN和注册码，成功系统给返回token，失败返回错误信息

设备注册信息包括：
- Device Name
- 
- Vender ID
- Vender Name
- Model Number
- Firmware version
- Firmware date

设备状态信息包括：
- 电池电量：多条记录，每条记录为{time:xxx, battery:xx}
- 故障信息：多条记录，每条记录为{time:xxx, info:xx}
- 使用统计：多条记录，每条记录为{time:xxx, info:xx}

