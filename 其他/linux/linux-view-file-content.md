# 查看文件内容

## 查看文件类型

目录

```bash
[root@server-test-211 kz]# file test
test: directory

```

文本

```bash
[root@server-test-211 kz]# file test.html
test.html: ASCII text

```

## 查看整个文件（内容）

> `cat`

| 选项 | 用途 |
|:-------|:-----|
| -n | 添加行号 |
| -b | 只给有文本的行添加行号|

```bash
[root@server-test-211 kz]# cat test.html
 a text file

```

```bash
[root@server-test-211 kz]# cat -n  test.html
     1	 a text file
     2	
     3	 hello world
     4	
     5	 hello linux
````

```bash
[root@server-test-211 kz]# cat -n  -b test.html
     1	 a text file

     2	 hello world

     3	 hello linux

```

## 查看部分文件

### 查看文件尾部内容

> `tail`

```bash

# 查看尾部 部分内容
[root@server-test-211 kz]# tail test.html
```

```bash

# 查看最后12行内容
[root@server-test-211 kz]# tail -n 12  test.html

```

### 查看文件头部内容

> `head`

```bash
[root@server-test-211 kz]# head test.html

```

```bash

#查看头部前三行内容
[root@server-test-211 kz]# head -3 test.html
 a text file

 hello world

```