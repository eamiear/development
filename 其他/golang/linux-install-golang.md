# golang 安装配置

## 下载golang包

```js
wget https://dl.google.com/go/go1.12.4.linux-amd64.tar.gz
```

## 解压到`/usr/local`

```js
tar -zxzf go1.12.4.linux-amd64.tar.gz  -C /usr/local
```

## 查看解压结果并验证

1. 进入`/usr/local`
   
   ```js
    [root@server-test-211 local]# cd /usr/local
    [root@server-test-211 local]# ll
    total 52
    drwxr-xr-x.  2 root root 4096 Apr 23 15:53 bin
    drwxr-xr-x.  2 root root 4096 Sep 23  2011 etc
    drwxr-xr-x.  2 root root 4096 Sep 23  2011 games
    drwxr-xr-x. 10 root root 4096 Apr 12 07:35 go
    drwxr-xr-x.  2 root root 4096 Apr 23 15:54 include
    drwxr-xr-x.  3 root root 4096 Apr 23 15:54 lib
    drwxr-xr-x.  2 root root 4096 Sep 23  2011 lib64
    drwxr-xr-x.  2 root root 4096 Sep 23  2011 libexec
    drwxr-xr-x. 11 root root 4096 Apr 29 14:55 nginx
    drwxr-xr-x.  6 root root 4096 Apr 23 15:56 openssl
    drwxr-xr-x.  2 root root 4096 Sep 23  2011 sbin
    drwxr-xr-x.  6 root root 4096 Apr 23 15:53 share
    drwxr-xr-x.  2 root root 4096 Sep 23  2011 src

   ```

2. 检测指令

    ```js
    [root@server-test-211 local]# cd go/bin
    [root@server-test-211 bin]# ./go version
    go version go1.12.4 linux/amd64

    ```

## 配置环境变量（全局使用）

1. 打开`profile`文件
   
   ```js
    [root@server-test-211 bin]# vim /etc/profile
   ```
2. 在底部添加以下配置内容
   
   ```js
    export GOPATH=/opt/go/gopath
    export GOROOT=/usr/local/go
    export GOARCH=386
    export GOOS=linux
    export GOTOOLS=$GOROOT/pkg/tool
    export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
   ```

3. 重新加载（刷新）`profile`文件
   
   ```js
    [root@server-test-211 bin]# source /etc/profile
   ```

4. 验证`go`命令
   
   ```js
    go version
   ```