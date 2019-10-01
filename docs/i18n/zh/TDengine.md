## 介绍

![TDengine官网介绍]()

## 安装

### docker 安装

注意： > 表示是在本机命令行中输入，$ 表示容器内

#### 1、获取源码

```
> git clone git@github.com:taosdata/TDengine.git
> cd TDengine
```

#### 2、创建 Dockerfile 文件

```
# Compile image
FROM centos as compile

WORKDIR /root

COPY src/ ./src/ 
COPY deps/ ./deps/
COPY packaging/ ./packaging/
COPY CMakeLists.txt ./

RUN yum update -y

RUN yum group install -y "Development Tools"

Run yum install -y cmake

WORKDIR /root/build
RUN cmake .. && cmake --build .

CMD ["bash"]

# Final image
FROM centos

WORKDIR /root

COPY --from=compile /root/build/build/bin /usr/bin/
COPY --from=compile /root/build/build/lib/libtaos.so /usr/lib/
COPY packaging/cfg/taos.cfg /etc/taos/

RUN echo "charset UTF-8" >> /etc/taos/taos.cfg

ENV LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/lib"
ENV LC_CTYPE="en_US.UTF-8"

CMD ["taosd"]
```

#### 3、生成镜像
```
> docker build -t tdtest .
```

#### 4、运行

运行时容器直接写 writable layer

```
> docker volume create td_log_vol
> docker volume create td_data_vol
```

启动服务

```
> docker run -itd --name tdtest_run  -v td_log_vol:/var/log/taos -v td_data_vol:/var/lib/taos tdtest
```

用 shell 访问容器
```
> docker exec -it tdtest_run bash
```

在容器内运行 taos

```
$ taos
```

[原文链接](https://blog.csdn.net/qishidiguadan/article/details/96284529)

## 表

首先在 TDengine 中，我们选用超级表（下简称：表）来存储我们的数据。

### 表结构

表结构即表中记录的数据列及其数据类型；

子表本质上就是普通的表，由一个时间戳主键和若干个数据列组成，每行记录着具体的数据，数据查询操作与普通表完全相同；

但子表与普通表的区别在于每个子表从属于一张超级表，并带有一组由STable定义的标签值。

### 标签

标签名和数据类型由表定义，标签值记录着每个子表的静态信息，用以对子表进行分组过滤。

标签信息属于Meta Data，如采集设备的序列号、型号、位置等，是静态的，是表的元数据。

### 表与设备间的联系

表与设备绑定：多功能设备的一次完整行为对应创建一张表，这种设备的一个实体创建一张字表。例如：型号为 MF47 的一款万用表创建一张表；一台 MF47 是这表下的一个字表
