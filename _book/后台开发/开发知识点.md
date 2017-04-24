# IP访问配置  端口修改
wamp 默认只能在服务机器上，通过 localhost来访问，默认端口为80，局域网内不能通过IP访问

## 端口修改
### 打开文件： wamp/bin/apache/apache2.4.9/config/httpd.conf

查询 ServerName
替换为如下：
ServerName localhost:5000

查询 Listen
将 Listen 80
替换为
Listen 5000

### 打开文件： wamp/wampmanager.tpl
查询 Parameter: "http://localhost/"

将 "http://localhost/" 改为 "http://localhost：5000/"
   "http://localhost/phpmyadmin/" 改为 "http://localhost：5000/phpmyadmin"
   "http://localhost/webgrind/" 改为 "http://localhost：5000/webgrind"


## IP访问配置

### 打开文件： wamp/bin/apache/apache2.4.9/config/httpd.conf
查询 Require local

将 Require local 改为 Require all granted
或者 Require ip 192.168.1.11（允许某个IP访问）