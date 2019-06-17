# 目录管理

## 创建目录

```bash
[root@server-test-211 kz]# mkdir user

[root@server-test-211 kz]# ls
admin.html  index.html  test  test.html  user

```

## 删除目录

| 选项 | 用途 |
|:-------|:-----|
| -r/-R | 递归删除|
| -f | 强制删除|

```bash
[root@server-test-211 kz]# rm -rf user

[root@server-test-211 kz]# ls
admin.html  index.html  test  test.html

```