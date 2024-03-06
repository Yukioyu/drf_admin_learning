# drf-admin 环境配置


## 软件安装

1、redis 安装

直接到github上下载安装包 https://github.com/tporadowski/redis/releases 

将下载的压缩包解压到指定的文件夹中，如：**D:\Redis**，内容如下：

![image-20240228192253662](image-20240228192253662.png)

在Redis的安装目录下打开cmd窗口，然后执行命令来启动服务：

```shell
redis-server.exe redis.windows.conf
```

> 可以打开cmd使用 cd 命令切换到redis所在的目录：`cd /d d:\redis`

随后使用`redis-server.exe redis.windows.conf`命令来启动redis服务：

![image-20240228192437608](image-20240228192437608.png)

> 默认端口为6379，出现图上的图标说明redis服务启动成功。命令里面的 redis.windows.conf 可以省略，省略后，使用redis-server.exe命令会使用默认的配置。

为了方便，建议把Redis路径配置到系统变量Path值中，这样就省得再输路径了。

我们使用`redis-cli.exe`命令来打开Redis客户端：

```shell
redis-cli.exe -h 127.0.0.1 -p 6379
```

在命令中输入ping命令来检测redis服务器与redis客户端的连通性，返回`PONG`则说明连接成功了。

> Tips:不要关闭redis服务端的cmd窗口

开启Redis空间通知功能，设置notify-keyspace-events KEA

首先要知道这个发送通知的操作是占内存的，所以默认的关闭的，需要我们手动的在redis.conf里面进行开启

如何开启：进入redis安装地址的/redis/etc文件下，可以使用文本编辑器打开修改“”为“KEA”即可。

2、python环境配置

直接使用`anaconda`的虚拟环境,执行以下命令：

```shell
conda create -n drf-admin python=3.6.2
```

然后使用`pip`借助requirements.txt进行安装，命令如下：

```shell
pip install -r requirements.txt
```



配置Django配置文件

​	默认使用SQLite，如使用MySQL，请更改settings/dev.py下的DATABASES参数

​	redis配置，配置settings/dev.py下REDIS_HOST、REDIS_PORT、REDIS_PWD等参数

数据库迁移

```shell
python manage.py migrate
```

初始化数据库基础数据

```shell
python manage.py loaddata init.json
```

启动Django项目

```shell
 python manage.py runserver 0.0.0.0:8769
```

