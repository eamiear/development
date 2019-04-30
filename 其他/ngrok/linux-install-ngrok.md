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

    [root@server-test-211 ngrok]# openssl genrsa -out rootCA.key 2048

    [root@server-test-211 ngrok]# openssl req -x509 -new -nodes -key rootCA.key -subj "/CN=$NGROK_DOMAIN" -days 5000 -out rootCA.pem

    [root@server-test-211 ngrok]# openssl genrsa -out device.key 2048

    [root@server-test-211 ngrok]# openssl req -new -key device.key -subj "/CN=$NGROK_DOMAIN" -out device.csr

    [root@server-test-211 ngrok]# openssl x509 -req -in device.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out device.crt -days 5000

   ```
3. 将新生成的证书替换，每条指令执行完后执行 `y`并回车
   ```
    
    [root@server-test-211 ngrok]# cp rootCA.pem assets/client/tls/ngrokroot.crt

    [root@server-test-211 ngrok]# cp device.crt assets/server/tls/snakeoil.crt

    [root@server-test-211 ngrok]# cp device.key assets/server/tls/snakeoil.key


   ```
4. 编译生成 `ngrokd` （服务端）
   ```
    [root@server-test-211 ngrok]# GOOS=linux GOARCH=amd64 make release-server
   ```
   生成在 `~/ngrok/bin/`目录中
5. 编译生成 `ngrok` （客户端）
   ```
    GOOS=windows GOARCH=amd64 make release-client
   ```
   生成在`~/ngrok/bin/windows_amd64/`目录中
6. 