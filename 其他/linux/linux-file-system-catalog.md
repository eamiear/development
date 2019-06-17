# Linux 文件系统目录

| 目录   | 用途  |
|:------ | :------|
| /     | 虚拟目录的根目录。通常不会在这里存储文件 |
| /bin  | 二进制目录，存放许多用户级的GNU工具 |
| /boot | 启动目录，存放启动文件 |
| /dev     | 设备目录，Linux在这里创建设备节点 |
| /etc     | 系统配置文件目录 |
| /home     | 主目录，Linux在这里创建用户目录 |
| /lib     | 库目录，存放系统和应用程序的库文件 |
| /media     | 媒体目录，可移动媒体设备的常用挂载点 |
| /mnt     | 挂载目录，另一个可移动媒体设备的常用挂载点 |
| /opt     | 可选目录，常用于存放第三方软件包和数据文件 |
| /proc     | 进程目录，存放现有硬件及当前进程的相关信息 |
| /root     | root用户的主目录 |
| /sbin     | 系统二进制目录，存放许多GNU管理员级工具 |
| /run     | 运行目录，存放系统运作时的运行时数据 |
| /srv     | 服务目录，存放本地服务的相关文件 |
| /sys     | 系统目录，存放系统硬件信息的相关文件 |
| /tmp     | 临时目录，可以在该目录中创建和删除临时工作文件 |
| /usr     | 用户二进制目录，大量用户级的GNU工具和数据文件都存储在这里 |
| /var     | 可变目录，用以存放经常变化的文件，比如日志文件 |

```bash
-rw-r--r--.   1 root root    0 May 10 12:21 1
lrwxrwxrwx.   1 root root    7 May 10 12:14 bin
dr-xr-xr-x.   4 root root 4096 May 10 12:35 boot
drwxr-xr-x.  20 root root 3300 May 10 12:33 dev
drwxr-xr-x. 134 root root 8192 May 14 15:15 etc
drwxr-xr-x.   7 root root   68 May 14 15:14 home
lrwxrwxrwx.   1 root root    7 May 10 12:14 lib
lrwxrwxrwx.   1 root root    9 May 10 12:14 lib64
drwxr-xr-x.   2 root root    6 Nov  5  2016 media
drwxr-xr-x.   2 root root    6 Nov  5  2016 mnt
drwxr-xr-x.   4 root root   30 May 10 14:02 opt
dr-xr-xr-x. 211 root root    0 May 10 12:33 proc
dr-xr-x---.   6 root root  233 May 10 14:14 root
drwxr-xr-x.  38 root root 1160 May 10 14:07 run
lrwxrwxrwx.   1 root root    8 May 10 12:14 sbin
drwxr-xr-x.   2 root root    6 Nov  5  2016 srv
dr-xr-xr-x.  13 root root    0 May 10 12:33 sys
drwxrwxrwt.  17 root root 4096 May 15 03:45 tmp
drwxr-xr-x.  13 root root  155 May 10 12:14 usr
drwxr-xr-x.  20 root root  282 May 10 12:33 var
```