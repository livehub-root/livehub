# LiveHub介绍

LiveHub是畜牧行业物联网应用中，IoT设备与云端对接的标准接口。LiveHub不仅提供了数据接口标准定义，而且提供了一个开源可部署实现实例。LiveHub的部署节点成为LiveHub Node，任何物联网云端服务可基于LiveHub快速接入设备，构建应用。

LiveHub的目的在于使得：
* 设备接⼊云服务，具有标准接⼝
* 设备产⽣的数据，具有标准格式

### 架构

* 数据库 ： [TDengine](https://github.com/taosdata/TDengine) >=1.6.2 [详情](./TDengine.md)
* 后　端 ： [Node.js](https://nodejs.org) >=10.16.3 ，[详情](https://github.com/livehub-root/livehub-node)
* 展　示 ： [php](https://www.php.net) >=7.2.23 ，[详情](https://github.com/livehub-root/livehub-php)
* 数据库中库与表：[参见]说明(./database.md)

### 接口

* [数据格式](./port/general.md)
* [设备](./port/device.md)
* [体重](./port/weight.md)
* [体高](./port/height.md)
* [图像](./port/image.md)
