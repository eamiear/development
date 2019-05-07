# linux 安裝nodejs

进入安装目录或资源目录
```bash
[root@server-test-211 ~]# cd /home/app/software/
```

下載node包

> 更多版本从这里获取 `https://nodejs.org/dist/`

```bash
[root@server-test-211 ~]# wget https://nodejs.org/dist/v8.11.3/node-v8.11.3-linux-x64.tar.xz
```

解压

```bash
[root@server-test-211 ~]# tar -xvf node-v8.11.3-linux-x64.tar.xz
```

移动到node目录（重命名）

```bash
[root@server-test-211 ~]# mv node-v8.11.3 nodejs
```

建立全局软链接

```bash
[root@server-test-211 ~]# sudo ln -s /home/kz/software/nodejs/bin/npm /usr/local/bin/npm
[root@server-test-211 ~]# sudo ln -s /home/kz/software/nodejs/bin/node /usr/local/bin/node
```

检测是否已安装
```bash
[root@server-test-211 ~]# node -v

[root@server-test-211 ~]# npm -v
```

删除软链

> 删除软链之前最好先把`nodejs`包删除

```bash
[root@server-test-211 ~]# rm -rf  /usr/local/bin/npm
[root@server-test-211 ~]# rm -rf  /usr/local/bin/node
```

安装 `cnpm`

执行指令：
```bash
[root@server-test-211 ~]# npm install -g cnpm --registry=https://registry.npm.taobao.org
```

结果：
```bash
[root@server-test-211 ~]# npm install -g cnpm --registry=https://registry.npm.taobao.org
/home/kz/software/nodejs/bin/cnpm -> /home/kz/software/nodejs/lib/node_modules/cnpm/bin/cnpm
+ cnpm@6.0.0
added 679 packages from 899 contributors in 12.415s

```

设置全局软连：

```bash
[root@server-test-211 ~]# ln -s /home/kz/software/nodejs/bin/cnpm /usr/local/bin/cnpm

```

验证：

```bash
[root@server-test-211 ~]# cnpm -v
cnpm@6.0.0 (/home/kz/software/nodejs/lib/node_modules/cnpm/lib/parse_argv.js)
npm@6.9.0 (/home/kz/software/nodejs/lib/node_modules/cnpm/node_modules/npm/lib/npm.js)
node@10.8.0 (/home/kz/software/nodejs/bin/node)
npminstall@3.21.0 (/home/kz/software/nodejs/lib/node_modules/cnpm/node_modules/npminstall/lib/index.js)
prefix=/home/kz/software/nodejs 
linux x64 2.6.32-696.el6.x86_64 
registry=https://registry.npm.taobao.org
```