# Jenkins安装配置

## Java环境

执行下面指令检查是否具备`Java`环境：
```bash
[root@server-test-211 ~]# java -version
```

如果存在，则无需下载安装；否则，执行下面指令执行安装：
```bash
[root@server-test-211 ~]# yum install java
```

## 安装Jenkins

分别执行下面指令：
```bash
[root@server-test-211 software]# wget -O /etc/yum.repos.d/jenkins.repo http://jenkins-ci.org/redhat/jenkins.repo
```
```bash
[root@server-test-211 software]# rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key
```
```bash
[root@server-test-211 software]# yum install jenkins
```

## 启动Jenkins

```bash
[root@server-test-211 software]# service jenkins start
```

## 可能存在的问题

### Java版本与Jenkins版本不一致

卸载系统Java版本：

1. 查询系统已安装的jdk
   ```bash
    [root@server-test-211 software]# rpm -qa|grep java
   ```
   ```bash
   [root@server-test-211 software]# rpm -qa|grep jdk
   ```
   ```bash
   [root@server-test-211 software]# rpm -qa|grep gcj
   ```
   ```bash
   [root@server-test-211 sbin]# rpm -qa|grep jdk
   java-1.6.0-openjdk-1.6.0.41-1.13.13.1.el6_8.x86_64
   java-1.7.0-openjdk-devel-1.7.0.131-2.6.9.0.el6_8.x86_64
   java-1.7.0-openjdk-1.7.0.131-2.6.9.0.el6_8.x86_64
   java-1.6.0-openjdk-javadoc-1.6.0.41-1.13.13.1.el6_8.x86_64
   java-1.6.0-openjdk-devel-1.6.0.41-1.13.13.1.el6_8.x86_64
   ```
   ```bash
   [root@server-test-211 sbin]# rpm -qa|grep jdk
   java-1.7.0-openjdk-devel-1.7.0.131-2.6.9.0.el6_8.x86_64
   java-1.7.0-openjdk-1.7.0.131-2.6.9.0.el6_8.x86_64
   java-1.6.0-openjdk-javadoc-1.6.0.41-1.13.13.1.el6_8.x86_64
   java-1.6.0-openjdk-devel-1.6.0.41-1.13.13.1.el6_8.x86_64
   ```
   ```bash
   [root@server-test-211 sbin]# rpm -qa|grep java
   libvirt-java-0.4.9-1.el6.noarch
   ant-javamail-1.7.1-15.el6.x86_64
   java-1.5.0-gcj-1.5.0.0-29.1.el6.x86_64
   eclipse-mylyn-java-3.4.2-9.el6.x86_64
   libvirt-java-devel-0.4.9-1.el6.noarch
   subversion-javahl-1.6.11-15.el6_7.x86_64
   tzdata-java-2016j-1.el6.noarch
   lpg-java-compat-1.1.0-4.1.el6.noarch
   java_cup-0.10k-5.el6.x86_64
   ```

2. 卸载已安装的jdk
   
   ```bash
   [root@server-test-211 sbin]# rpm -e --nodeps java-1.6.0-openjdk-1.6.0.41-1.13.13.1.el6_8.x86_64
   [root@server-test-211 sbin]# rpm -e --nodeps java-1.7.0-openjdk-1.7.0.131-2.6.9.0.el6_8.x86_64
   [root@server-test-211 sbin]# rpm -e --nodeps java-1.7.0-openjdk-devel-1.7.0.131-2.6.9.0.el6_8.x86_64
   [root@server-test-211 sbin]# rpm -e --nodeps java-1.6.0-openjdk-devel-1.6.0.41-1.13.13.1.el6_8.x86_64
   [root@server-test-211 sbin]# rpm -e --nodeps java-1.5.0-gcj-1.5.0.0-29.1.el6.x86_64
   ```
3. 验证是否还有jdk
   ```bash
    [root@server-test-211 sbin]# rpm -qa|grep java
    [root@server-test-211 sbin]# java -version
    -bash: /usr/bin/java: No such file or directory
   ```
4. 重新安装jdk
   ```bash
   [root@server-test-211 sbin]# yum install java
   ```

### 卸载Jenkins

1. 卸载
   ```bash
    [root@server-test-211 sbin]# rpm -e jenkins
   ```
2. 检查是否卸载成功
   ```bash
    [root@server-test-211 sbin]# rpm -ql jenkins
   ```
3. 删除残留文件
   
   ```bash
    [root@server-test-211 sbin]# find / -iname jenkins | xargs -n 1000 rm -rf
   ```

### Jenkins执行报错

> `java.net.UnknownHostException: server-test-211`

```bash
[root@server-test-211 /]# vim /var/log/jenkins/jenkins.log

        at jenkins.security.ImpersonatingExecutorService$2.call(ImpersonatingExecutorService.java:71)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
        at java.lang.Thread.run(Thread.java:748)
Caused by: java.net.UnknownHostException: server-test-211: Name or service not known
        at java.net.Inet6AddressImpl.lookupAllHostAddr(Native Method)
        at java.net.InetAddress$2.lookupAllHostAddr(InetAddress.java:929)
        at java.net.InetAddress.getAddressesFromNameService(InetAddress.java:1324)
        at java.net.InetAddress.getLocalHost(InetAddress.java:1501)
        ... 10 more

```


解决方法：在`/etc/hosts`中添加`server-test-211`,如：

```bash
[root@server-test-211 /]# vim /etc/hosts

127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
127.0.0.1   server-test-211
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
```

### 查看防火墙
```bash
[root@server-test-211 sbin]# vi /etc/sysconfig/iptables
```


## 通过 `Tomcat` 安装 `Jenkins`
