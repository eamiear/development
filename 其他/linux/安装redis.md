# linux安装redis

0. 进入安装目录
cd /home/app/software

1. 下载redis资源
wget http://download.redis.io/releash/redis-4.0.8.tar.gz

2. 解压
tar xzvf redis-4.0.8.tar.gz

3. 重命名
mv redis-4.0.8 redis

4. 安装
1) cd redis
make

2) 安装的全局
cd src
make install PREFIX=/usr/local/redis

5. 配置文件复制到安装目录
cd /usr/local/redis/
mkdir etc
mv /home/app/software/redis/redis.conf /usr/local/redis/etc

6. 配置redis为后台启动
vi /usr/local/redis/etc/redis.conf

// 将 daemonize no 改为为 daemonize yes

7. 配置redis密码
vi /usr/local/redis/etc/redis.conf

// 在[sercury] 项下找到 requirepass
// 取消注释并将 requirepass foobared 改为 requirepass “123456”

8. 启动redis服务
/usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf

9. 开机启动redis服务
vi /etc/rc.local
添加 /usr/local/redis/bin/redis-server /usr/local/redis/etc/reids.conf

10. 启动redis-cli检测是否启动成功（1）
cd /usr/local/redis/bin/
./redis-cli

1) 查看密码： config get requirepass, 如果返回NOAUTH Authentication required错误，则登录
2) 登录： auth "123456"，返回OK即登录成功
3) 设置缓存数据

11. 检测redis是否启动(2)
1) 进程检测：ps -ef | grep redis
2) 端口检测： netstat -lntp | grep 6379

12. 停止redis服务
1) redis-cli shutdown
2) ps -ef | grep redis
   kill [进程pid]

13. 卸载redis
1) rm -rf /usr/local/redis  // 删除安装目录
2) rm -rf /usr/bin/redis-*  // 删除所有redis命令
3) rm -rf /home/app/software/redis*
