# 文件和目录列表指令 `ls`

| 选项 | 用途 |附加说明|示例|
|:-------|:-----|-----|----|
| | 安按字母排序输出列表|||
| `-F` | 区分文件和目录 |||
| `-a` | 输出隐藏文件 |||
| `-R` | 递归输出子目录的文件 |||
| `-l` | 列表格式输出及其详细信息 |||
| `?` | 过滤输出列表，表示一个字符 |文件拓展匹配||
| `*` | 过滤输出列表，表示零个或多个字符 |文件拓展匹配||
| `[]` | 过滤输出列表，表示零个或多个字符 |元字符统配符|`[axo]、[a-z]`|
| `[!]` | 过滤输出列表，排除在外的内容 |元字符统配符|`[!a]`|

```bash
[root@server-test-211 /]# ls
1  bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```

```bash
[root@server-test-211 /]# ls -F
1     boot/  etc/   lib@    media/  opt/   root/  sbin@  sys/  usr/
bin@  dev/   home/  lib64@  mnt/    proc/  run/   srv/   tmp/  var/
```

```bash
[root@server-test-211 /]# ls -a
.   1    boot  etc   lib    media  opt   .readahead  run   srv  tmp  var
..  bin  dev   home  lib64  mnt    proc  root        sbin  sys  usr
```

```bash
[root@server-test-211 kz]# ls -F -R
.:
test/  test.md

./test:
index.md
```

```bash
[root@server-test-211 kz]# ls -l
total 4
drwxr-xr-x. 2 root root 22 May 15 15:53 test
-rw-r--r--. 1 root root 13 May 15 15:52 test.md
```

```bash
[root@server-test-211 kz]# ls -l t?st.md
-rw-r--r--. 1 root root 13 May 15 15:52 test.md
```

```bash
[root@server-test-211 kz]# ls -l t*.md
-rw-r--r--. 1 root root 13 May 15 15:52 test.md

```

```bash
[root@server-test-211 kz]# ls -l te[xi]t.md
-rw-r--r--. 1 root root 13 May 15 16:07 text.md
```

```bash
[root@server-test-211 kz]# ls -l te[xs]t.md
-rw-r--r--. 1 root root 13 May 15 15:52 test.md
-rw-r--r--. 1 root root 13 May 15 16:07 text.md
```

```bash
[root@server-test-211 kz]# ls -l te[a-z]t.md
-rw-r--r--. 1 root root 13 May 15 15:52 test.md
-rw-r--r--. 1 root root 13 May 15 16:07 text.md
```

```bash
[root@server-test-211 kz]# ls -l te[!x]t.md
-rw-r--r--. 1 root root 13 May 15 15:52 test.md
```