# Linux 安装 gitlab

## 系统环境

```bash
[root@server-test-211 ~]# head -n 1 /etc/issue
CentOS release 6.9 (Final)

```

## 安装配置依赖

```bash
[root@server-test-211 ~]# sudo yum install -y curl policycoreutils-python openssh-server cronie

# 防火墙开启 HTTP 和 SSH 权限
[root@server-test-211 ~]# sudo lokkit -s http -s ssh
```

## 安装邮件服务

```bash
[root@server-test-211 ~]# sudo yum install postfix
[root@server-test-211 ~]# sudo service postfix start
[root@server-test-211 ~]# sudo chkconfig postfix on

```

## 添加 gitlab 仓库包

```bash
[root@server-test-211 ~]# curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash

```

## 安装 gitlab

可在安装时设置外部访问链接
```bash
[root@server-test-211 ~]# sudo EXTERNAL_URL="http://gitlab.example.com" yum -y install gitlab-ce

```

## 安装成功效果
```
Running handlers:
Running handlers complete
Chef Client finished, 476/1265 resources updated in 02 minutes 33 seconds
gitlab Reconfigured!

       *.                  *.
      ***                 ***
     *****               *****
    .******             *******
    ********            ********
   ,,,,,,,,,***********,,,,,,,,,
  ,,,,,,,,,,,*********,,,,,,,,,,,
  .,,,,,,,,,,,*******,,,,,,,,,,,,
      ,,,,,,,,,*****,,,,,,,,,.
         ,,,,,,,****,,,,,,
            .,,,***,,,,
                ,*,.
  


     _______ __  __          __
    / ____(_) /_/ /   ____ _/ /_
   / / __/ / __/ /   / __ `/ __ \
  / /_/ / / /_/ /___/ /_/ / /_/ /
  \____/_/\__/_____/\__,_/_.___/
  

Thank you for installing GitLab!
GitLab should be available at http://gitlab.on-bright.com

For a comprehensive list of configuration options please see the Omnibus GitLab readme
https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/README.md

  Verifying  : gitlab-ce-11.10.4-ce.0.el6.x86_64                                                                                                       1/1 

Installed:
  gitlab-ce.x86_64 0:11.10.4-ce.0.el6                                                                                                                      

Complete!
```
## 浏览器查看

默认 80 端口
```
http://gitlab.example.com
```

## 使用系统已有 NGINX 服务



## 常见问题

### gitlab 安装时，包下载超时

<code style="color: red">

===========================================================================================================================================================

Install       1 Package(s)

Total download size: 581 M
Installed size: 1.5 G
Downloading Packages:
https://packages.gitlab.com/gitlab/gitlab-ce/el/6/x86_64/gitlab-ce-11.10.4-ce.0.el6.x86_64.rpm: [Errno 12] Timeout on https://packages-gitlab-com.s3-accelerate.amazonaws.com/7/8/el/6/package_files/40781.rpm?AWSAccessKeyId=AKIAJ74R7IHMTQVGFCEA&Signature=yxzcDoC9zmCo8O8loX2YqCtQCes%3D&Expires=1557307214: (28, 'Operation too slow. Less than 1 bytes/sec transfered the last 30 seconds')
Trying other mirror.


Error Downloading Packages:
  gitlab-ce-11.10.4-ce.0.el6.x86_64: failure: gitlab-ce-11.10.4-ce.0.el6.x86_64.rpm from gitlab_gitlab-ce: [Errno 256] No more mirrors to try.

</code>

#### 镜像切换

##### 新建镜像 repo 

新建镜像 repo 并填入内容

```bash
[root@iZbp19xg5vv2b5wnt0avavZ ~]# vi /etc/yum.repos.d/gitlab-ce.repo

[gitlab-ce]
name=Gitlab CE Repository
baseurl=https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el$releasever/
gpgcheck=0
enabled=1

```
重新进入安装步骤

##### 参考
[Gitlab Community Edition 镜像使用帮助](https://mirror.tuna.tsinghua.edu.cn/help/gitlab-ce/)
