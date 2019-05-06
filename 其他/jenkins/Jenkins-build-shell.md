# Jenkins 构建 shell 脚本

## 本地服务
```bash
cd /root/.jenkins/workspace/github_test
cnpm install
cnpm run build
echo
echo "Begin to Clean Old Files"
echo

rm -rf /home/kz/server/nginx/html/github_test/*
cp -r /root/.jenkins/workspace/github_test/dist/* /home/kz/server/nginx/html/github_test/

```

> `/root/.jenkins/workspace/github_test` 为 `Jenkins`默认项目代码存放地址，可通过 `JENKINS_HOME` 修改。
> 
> `rm -rf /home/kz/server/nginx/html/github_test/*` 清除 `nginx` 服务下 `github_test` 项目中的内容
> 
> `cp -r /root/.jenkins/workspace/github_test/* /home/kz/server/nginx/html/github_test/` 将 `jenkins` 源码工程的目标资源复制到 `nginx` 对应的目录下

## 远程服务

> 将一台服务器中子源拷贝到其他机器上，即 Jenkins 与 nginx 分别部署在不同的服务器上。


```bash
ssh -o StrictHostKeyChecking=no root@192.168.200.211 'rm -rf /home/kz/server/nginx/html/github_test/*'

scp -r /root/.jenkins/workspace/github_test/* /home/kz/server/nginx/html/github_test/
```

## 参考

[ssh免密码登录](http://www.cnblogs.com/xubing-613/p/6844564.html)