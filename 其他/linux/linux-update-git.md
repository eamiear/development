# Linux 更新 git 版本

## 查看 git 版本， 并卸载
```bash
[root@server-test-211 ~]# git --version

[root@server-test-211 ~]# yum remove git
```

## 安装依赖软件（如已经安装过git，跳过）

```bash
[root@server-test-211 ~]# yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel asciidoc
[root@server-test-211 ~]# yum install  gcc perl-ExtUtils-MakeMaker

```

## 编译安装最新的 git 版本

> 可选指定安装版本 `https://mirrors.edge.kernel.org/pub/software/scm/git/`

```bash
[root@server-test-211 ~]# cd /usr/local/src/
[root@server-test-211 ~]# wget -O git.zip https://github.com/git/git/archive/master.zip
[root@server-test-211 ~]# unzip git.zip
[root@server-test-211 ~]# cd git-master
[root@server-test-211 ~]# make prefix=/usr/local/git all
[root@server-test-211 ~]# make prefix=/usr/local/git install
```

## 添加变量到环境

```bash
[root@server-test-211 ~]# echo "export PATH=$PATH:/usr/local/git/bin" >> ~/.bashrc
[root@server-test-211 ~]# source ~/.bashrc
[root@server-test-211 ~]# git --version
```

## git 使用常见问题

1. git 版本过低

```
error: The requested URL returned error: 401 Unauthorized while accessing https://git.oschina.net/zemo/demo.git/info/refs 
fatal: HTTP request failed
```