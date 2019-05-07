# Linux 指令

## vi 指令： 打开、编辑文件

> 如编辑hosts文件   ```vi /etc/hosts```

1. 打开文件
```bash
vi /etc/hosts
```

2. 修改文件

    点击键盘```Insert```键，切换到修改状态

3. 修改文件后，退出修改状态

    点击键盘```Esc```键，退出编辑状态

4. 保存修改内容
:w + Enter(回车)

## 保存操作其他指令：

1. :w 保存文件但不退出 vi
2. :w file 将修改保存到file中，不退出vi
3. :w! 强制保存，不退出 vi
4. :wq 保存文件并退出 vi
5. :wq! 强制保存文件， 并退出 vi
6. :q 不保存文件，退出 vi
7. :q! 不保存文件，强制退出 vi
8. :e! 放弃所有修改

5. 退出 vi 编辑界面
```bash
[root@server-test-211 ~]# :quit + Enter(回车)

[root@server-test-211 ~]# :q
```

## 文件操作相关

1. 创建文件夹
```bash
[root@server-test-211 ~]#  mkdir [文件夹名称]
```
2. 删除文件夹
```bash
[root@server-test-211 ~]# rm -rf [文件夹名称]
```

3. 创建文件
   - vi [文件]	 `// vi readme.txt`
   - 输入内容
   - 退出输入并保存内容
   - 退出编辑

4. 删除文件
```bash
[root@server-test-211 ~]# rm [文件名称]
```


## 软链

创建软链

```bash
[root@server-test-211 ~]#  ln -S /home/kz/software/node/bin/node /usr/local/bin/node
```

或

```bash
[root@server-test-211 ~]# ln -s /home/kz/software/node/bin/node /usr/local/bin/
```

删除软链

```bash
[root@server-test-211 ~]# rm -rf /usr/local/bin/node
```

## 获取当前目录

```bash
[root@server-test-211 bin]# pwd
/home/kezai/apache-tomcat-8.5.40/bin
```

