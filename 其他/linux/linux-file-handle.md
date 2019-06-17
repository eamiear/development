# 文件处理

## 创建文件

```bash
[root@server-test-211 kz]# touch admin.html
```

```bash
[root@server-test-211 kz]# ls -l
total 12
-rw-r--r--. 1 root root  0 May 15 16:13 admin.html
-rw-r--r--. 1 root root 13 May 15 16:06 index.html
drwxr-xr-x. 2 root root 22 May 15 15:53 test
-rw-r--r--. 1 root root 13 May 15 15:52 test.md
-rw-r--r--. 1 root root 13 May 15 16:07 text.md
```

## 复制文件

`cp source destination`
> 将 source 复制到 destination，如果destination为文件名路径，则为覆盖操作

```bash
[root@server-test-211 kz]# ls
admin.html  index.html  test  test.md  text.md

[root@server-test-211 kz]# cp index.html test/
[root@server-test-211 test]# ls
index.html  index.md

# 复制并重新命名
[root@server-test-211 kz]# cp admin.html test/admin.md
[root@server-test-211 test]# ls
admin.md  index.html  index.md

# 覆盖
[root@server-test-211 kz]# cp index.html test/admin.md
cp: overwrite ‘test/admin.md’? y

# 复制所有test目录下所有文件到 user 目录
[root@server-test-211 kz]# cp test/* user/
[root@server-test-211 kz]# cd user
[root@server-test-211 user]# ls
admin.md  index.html  index.md
```

## 文件重命名

```bash
[root@server-test-211 kz]# mv text.md test.html

```

重命名并移动

```bash
[root@server-test-211 kz]# mv test.md ./user/user.md

[root@server-test-211 user]# ls
admin.md  index.html  index.md  user.md
```

## 删除文件

| 选项 | 用途 |
|:-------|:-----|
| `-i` | 提示是否要删除文件 |
| `-f` | 强制删除文件 |

```bash
[root@server-test-211 user]# rm user.md
rm: remove regular file ‘user.md’? y

```

```bash
[root@server-test-211 user]# rm -f index.md
```
