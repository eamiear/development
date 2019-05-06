# ngrok安装配置

## 安装环境
检测 `gcc` 和 `git` 是否已安装（用于下载ngrok源码）

```
[root@server-test-211 home]# gcc -v

[root@server-test-211 home]# git -v

```

如果没有安装，则进行安装

```
[root@server-test-211 home]# yum install gcc -y

[root@server-test-211 home]# yum install git -y
```

## 安装 `go` 语言环境

> [安装golang](../golang/linux-install-golang.md)

## 在服务器搭建`ngrok`服务

1. 下载`ngrok`源码
   ```
    [root@server-test-211 server]# git clone https://github.com/inconshreveable/ngrok.git
   ```
2. 生成证书
   
   ```
    [root@server-test-211 server]# cd ngrok

   ```

    配置域名：
   ```
    [root@server-test-211 ngrok]# export NGROK_DOMAIN="tunnel.ob.me"

    [root@server-test-211 ngrok]# openssl genrsa -out base.key 2048

    [root@server-test-211 ngrok]# openssl req -x509 -new -nodes -key base.key -subj "/CN=$NGROK_DOMAIN" -days 5000 -out base.pem

    [root@server-test-211 ngrok]# openssl genrsa -out server.key 2048

    [root@server-test-211 ngrok]# openssl req -new -key server.key -subj "/CN=$NGROK_DOMAIN" -out server.csr

    [root@server-test-211 ngrok]# openssl x509 -req -in server.csr -CA base.pem -CAkey base.key -CAcreateserial -out server.crt -days 5000

   ```
3. 将新生成的证书替换，每条指令执行完后执行 `y`并回车
   ```
    
    [root@server-test-211 ngrok]# cp base.pem assets/client/tls/ngrokroot.crt

    [root@server-test-211 ngrok]# cp server.crt assets/server/tls/snakeoil.crt

    [root@server-test-211 ngrok]# cp server.key assets/server/tls/snakeoil.key


   ```
4. 编译生成 `ngrokd` （服务端）
   ```
    [root@server-test-211 ngrok]# GOOS=linux GOARCH=amd64 make release-server
    GOOS="" GOARCH="" go get github.com/jteeuwen/go-bindata/go-bindata
    bin/go-bindata -nomemcopy -pkg=assets -tags=release \
            -debug=false \
            -o=src/ngrok/client/assets/assets_release.go \
            assets/client/...
    bin/go-bindata -nomemcopy -pkg=assets -tags=release \
            -debug=false \
            -o=src/ngrok/server/assets/assets_release.go \
            assets/server/...
    go get -tags 'release' -d -v ngrok/...
    go install -tags 'release' ngrok/main/ngrokd
    go install -tags 'release' ngrok/main/ngrok
   ```
   或者服务端、客户端一起生成
   ```
    [root@server-test-211 ngrok]# make release-server release-client
   ```
   生成在 `~/ngrok/bin/`目录中


   > 如果 `GOOS=linux GOARCH=amd64` 无法设置 `go` 配置信息，可执行以下指令
   ```
    export GOOS=linux
    export GOARCH=amd64
   ```
   然后通过`go env`查看配置信息
   ```go
    [root@server-test-211 ngrok]# go env
    GOARCH="amd64"
    GOBIN=""
    GOCACHE="/root/.cache/go-build"
    GOEXE=""
    GOFLAGS=""
    GOHOSTARCH="amd64"
    GOHOSTOS="linux"
    GOOS="linux"
    GOPATH="/home/kz/ngrok"
    GOPROXY=""
    GORACE=""
    GOROOT="/usr/local/go"
    GOTMPDIR=""
    GOTOOLDIR="/usr/local/go/pkg/tool/linux_amd64"
    GCCGO="gccgo"
    CC="gcc"
    CXX="g++"
    CGO_ENABLED="1"
    GOMOD=""
    CGO_CFLAGS="-g -O2"
    CGO_CPPFLAGS=""
    CGO_CXXFLAGS="-g -O2"
    CGO_FFLAGS="-g -O2"
    CGO_LDFLAGS="-g -O2"
    PKG_CONFIG="pkg-config"
    GOGCCFLAGS="-fPIC -m64 -pthread -fmessage-length=0 -fdebug-prefix-map=/tmp/go-build668421739=/tmp/go-build"
   ```

5. 编译生成 `ngrok` （客户端）
   ```
    GOOS=windows GOARCH=amd64 make release-client
   ```
   生成在`~/ngrok/bin/windows_amd64/`目录中
   ```
    -rwxr-xr-x. 1 root root  2893387 May  6 10:11 go-bindata
    -rwxr-xr-x. 1 root root 12953899 May  6 10:11 ngrok
    -rwxr-xr-x. 1 root root 10271251 May  6 10:11 ngrokd
   ```
6. 设置域名解析
   
7. 运行 `Ngrok`
   
   ```
    [root@server-test-211 ngrok]# ./bin/ngrokd -tlsKey=server.key -tlsCrt=server.crt -domain="tunnel.ob.me" -httpAddr=":9000" -httpsAddr=":9001"
    [10:27:01 CST 2019/05/06] [INFO] (ngrok/log.(*PrefixLogger).Info:83) [metrics] Reporting every 30 seconds
    [10:27:01 CST 2019/05/06] [INFO] (ngrok/log.(*PrefixLogger).Info:83) [registry] [tun] No affinity cache specified
    [10:27:01 CST 2019/05/06] [INFO] (ngrok/log.Info:112) Listening for public http connections on [::]:9000
    [10:27:01 CST 2019/05/06] [INFO] (ngrok/log.Info:112) Listening for public https connections on [::]:9001
    [10:27:01 CST 2019/05/06] [INFO] (ngrok/log.Info:112) Listening for control and proxy connections on [::]:4443

   ```
   服务端启动(后台运行)：
   ```
    nohup ngrokd -domain="tunnel.ob.me" -httpAddr=":9000" &
   ```

8. 开机自动启动ngrok服务
   ```vim
    [root@server-test-211 ~]# vi /etc/init.d/ngrok_start
    # 加入下面内容
    cd /home/kezai/ngrok/
    ./bin/ngrokd -tlsKey=server.key -tlsCrt=server.crt -domain="tunnel.ob.me" -httpAddr=":9000" -httpsAddr=":9001"
    chmod 755 /etc/init.d/ngrok_start

   ```
9.  



## 参考
[linux下ngrok配置和使用](https://blog.csdn.net/daiqi5527153/article/details/78629359)