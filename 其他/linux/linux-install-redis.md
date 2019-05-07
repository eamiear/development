# linux安装redis

0. 进入安装目录
 
```bash
[root@server-test-211 ~]# cd /home/app/software
```

1. 下载redis资源

```bash
[root@server-test-211 software]# wget http://download.redis.io/releash/redis-4.0.8.tar.gz
```

2. 解压

```bash
[root@server-test-211 software]# tar xzvf redis-4.0.8.tar.gz
```

3. 重命名

```bash
[root@server-test-211 software]# mv redis-4.0.8 redis
```

4. 安装

```bash
[root@server-test-211 software]# cd redis
[root@server-test-211 redis]# make
```

安装的全局
```bash
[root@server-test-211 redis]# cd src
[root@server-test-211 src]# make install PREFIX=/usr/local/redis
```

5. 配置文件复制到安装目录

```bash   
[root@server-test-211 src]# cd /usr/local/redis/
[root@server-test-211 redis]# mkdir etc
[root@server-test-211 redis]# mv /home/app/software/redis/redis.conf /usr/local/redis/etc
```

6. 配置 redis 为后台启动

>将 `daemonize no `改为为 `daemonize yes`

```bash
[root@server-test-211 redis]# vi /usr/local/redis/etc/redis.conf
```

7. 配置 redis 密码

```bash
[root@server-test-211 redis]# vi /usr/local/redis/etc/redis.conf
```

> 在`[sercury]` 项下找到 `requirepass `
>
> 取消注释并将 `requirepass foobared` 改为 `requirepass “123456”`


8. 启动 redis 服务

```bash
[root@server-test-211 redis]# /usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf
```

9. 开机启动 redis 服务

```bash
[root@server-test-211 redis]# vi /etc/rc.local
```

> 添加 `/usr/local/redis/bin/redis-server /usr/local/redis/etc/reids.conf`


10. 启动 redis-cli 检测是否启动成功（1）

```bash
[root@server-test-211 redis]# cd /usr/local/redis/bin/
[root@server-test-211 bin]# ./redis-cli

```
> 1)  查看密码： `config get requirepass`, 如果返回 `NOAUTH Authentication required` 错误，则登录
> 2)  登录： `auth "123456"`，返回 `OK` 即登录成功
> 3)  设置缓存数据

11. 检测 redis 是否启动(2)

1) 进程检测
```bash
[root@server-test-211 bin]# ps -ef | grep redis
```
2) 端口检测

```bash
[root@server-test-211 bin]# netstat -lntp | grep 6379
```

12. 停止 redis 服务
```bash 
[root@server-test-211 bin]# redis-cli shutdown
[root@server-test-211 bin]# ps -ef | grep redis
[root@server-test-211 bin]# kill [进程pid]
```
13. 卸载 redis

```bash
[root@server-test-211 bin]# rm -rf /usr/local/redis  // 删除安装目录
[root@server-test-211 bin]# rm -rf /usr/bin/redis-*  // 删除所有redis命令
[root@server-test-211 bin]# rm -rf /home/app/software/redis*
```
