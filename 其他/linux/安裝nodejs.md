# linux 安裝nodejs

进入安装目录或资源目录
```
cd /home/app/software/
```

下載node包

> 更多版本从这里获取 `https://nodejs.org/dist/`

```
wget https://nodejs.org/dist/v8.11.3/node-v8.11.3-linux-x64.tar.xz
```

解压
```
tar -xvf node-v8.11.3-linux-x64.tar.xz
```

移动到node目录（重命名）
```
mv node-v8.11.3 nodejs
```

建立全局软链接
```
[root@server-test-211 ~]# sudo ln -s /home/kz/software/nodejs/bin/npm /usr/local/bin/npm
[root@server-test-211 ~]# sudo ln -s /home/kz/software/nodejs/bin/node /usr/local/bin/node
```

检测是否已安装
```
node -v

npm -v
```

删除软链

> 删除软链之前最好先把`nodejs`包删除

```
[root@server-test-211 ~]# rm -rf  /usr/local/bin/npm
[root@server-test-211 ~]# rm -rf  /usr/local/bin/node
```

安装 `cnpm`

```
npm install -y cnpm
```