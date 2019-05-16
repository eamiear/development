# 进程管理

## 查看进程

> `ps`

| 选项 | 用途 |
|:-------|:-----|
|  | 默认查看当前控制台下当前用户的进程 |
| -A | 显示所有进程|
| -N | 显示与指定参数不符的所有进程|
| -a | 显示除控制进程和无终端进程外的所有进程|
| -d | 显示除控制进程外的所有进程|
| -e | 显示所有进程|
| -C cmdlist | 显示包含在cmdlist列表中的进程|
| -G grplist | 显示组ID在grplist列表中的进程|
| -U userlist | 显示属主的用户ID在userlist列表中的进程|
| -g grplist | 显示会话或组ID在grplist列表中的进程|
| -p pidlist | 显示PID在pidlist列表中的进程|
|-s sesslist | 显示会话ID在sesslist列表中的进程|
|-t ttylist  |显示终端ID在ttylist列表中的进程|
|-u userlist |显示有效用户ID在userlist列表中的进程|
|-F |显示更多额外输出（相对-f参数而言）|
|-O format |显示默认的输出列以及format列表指定的特定列|
|-M |显示进程的安全信息|
|-c |显示进程的额外调度器信息|
|-f |显示完整格式的输出|
|-j |显示任务信息|
|-l |显示长列表|
|-o format |仅显示由format指定的列|
|-y |不要显示进程标记（process flag，表明进程状态的标记）|
|-Z |显示安全标签（security context）①信息|
|-H |用层级格式来显示进程（树状，用来显示父进程）|
|-n namelist |定义了WCHAN列显示的值|
|-w |采用宽输出模式，不限宽度显示|
|-L |显示进程中的线程|
|-V |显示ps命令的版本号|

```bash
[root@server-test-211 kz]# ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 May10 ?        00:00:14 /usr/lib/systemd/systemd --system --deserialize 17

```

## 结束进程

### 结束指定PID进程

```bash
[root@server-test-211 kz]# kill [PID]
```

### 结束所有进程

```bash
[root@server-test-211 kz]# killall
```

```bash

# 结束所有匹配的进程
[root@server-test-211 kz]# killall http*
```