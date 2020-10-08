# Linux 命令行简介
## Linux 命令行概述
### Linux 命令行的作用与意义
1. `Linux`是一个主要通过命令行来进行管理的操作系统，即通过键盘输入指令来管理系统的相关操作，包括但不限于编辑文件、启动停止服务等。
2. 使用`Linux`命令行管理，不但可以批量、自动化管理，而且还可以实现智能化、可视化管理。
### Linux 命令行介绍
1. 安装`Linux`系统时候，无论是使用文本模式(命令行)安装，还是使用图形模式安装，最终管理系统的任务都会落到命令行之上。
### Linux 命令行的开启和退出
1. 在开启主机之后，`Linux`系统会经过一系列的引导和程序加载，最终会出现相应的登录前的提示界面，将光标定位到`“login:”`字符串后面，输入超级用户管理员`root`之后，按回车键，弹出密码提示框后再输入密码，注意密码是不显示的。输入了正确的密码之后，再按回车键就可以登录到`Linux`系统中了。
2. 在命令执行`exit`或`logout`命令可退出命令行，当然也可以使用快捷键`ctrl+d`退出命令行，退出命令行之后，如果需要再次登录，则还是需要输入用户名和密码(除非使用`SSH客户端`已将用户名和密码保存起来了)。
### Linux 命令行提示符介绍
1. `Linux`命令行结尾的提示符有`“#”`和`“$”`两种不同的符号，代码如下：
```
[root@oldboy ~]#        #<==这是超级管理员root用户对应的命令行。
[oldboy@oldboy ~]c      #<==这是普通用户oldboy对应的命令行。
```
2. 其中`“#”`号，是使用超级用户`root`登录后的命令行结尾提示符，而`“$”`号是使用普通用户登录后的命令行结尾提示符。
3. 超级用户具有管理系统的所有权限，普通用户的权限比较小，只能进行基本的系统信息查看等操作，无法更改系统配置和管理服务。
4. 命令行提示符`@`前面的字符代表当前登录的用户(可用`whoami`查询)，@后面的为主机名(可用`hostname`查询)，`~`所在的位置是窗口当前用户所在的路径。示例代码如下：
```
[oldboy@oldboy ~]$      #<==@前的oldboy为当前用户，@后的oldboy为主机名，此处的~表示当前目录，即家目录。
```
5. `Linux`命令提示符由`PS1`环境变量控制。示例代码如下：
```
[root@oldboy ~]# set|grep PS1      #<==注意PS1是大写的
PS1='[\u@\h \W]\$'                 #<==等号后特殊变量的讲解见特殊变量表
```
6. 这里的`PS1='[\u@\h\W]\$'`，可以通过全局配置文件`/etc/bashrc`或`/etc/profile`进行按需配置和调整。
### Linux 命令行常用快捷键
1. 在企业工作中，管理`Linux`时一般不会直接采用键盘、显示器登录系统，而是会通过网络在远程进行管理，因此，需要通过远程连接工具连接到`Linux`系统中。
2. 目前最常用的`Linux`远程连接工具为：`SecureCRT`和`Xshell`客户端软件。
3. 下表展示的是提高`Linux`运维效率的30个命令行常用快捷键：

|快捷键|功能说明(*为常用)|
|--|--|
|最有用快捷键|
|`tab`|命令或路径等的补全键，`Linux`最有用的快捷键*|
|移动光标快捷键||
|`Ctrl+a`|光标回到命令行行首*|
|`Ctrl+e`|光标回到命令行行尾*|
|`Ctrl+f`|光标向右移动一个字符(相当于方向键的右键)|
|`Ctrl+b`|光标向左移动一个字符(相当于方向键的左键)|
|剪切、粘贴、清除快捷键||
|`Ctrl+Insert`|复制命令行内容*|
|`Shfit+Insert`|粘贴命令行内容*|
|`Ctrl+k`|剪切(删除)光标处到行尾的字符*|
|`Ctrl+u`|剪切(删除)光标处到行首的字符*|
|`Ctrl+w`|剪切(删除)光标前的一个单词|
|`Ctrl+y`|粘贴`Ctrl+u/Ctrl+k/Ctrl+w`删除的文本|
|`Ctrl+c`|中断终端正在执行的任务或者删除整行*|
|`Ctrl+h`|删除光标所在处的前一个字符(相当于退格键)|
|重复执行命令快捷键||
|`Ctrl+d`|退出当前`Shell`命令行*|
|`Ctrl+r`|搜索命令行使用过的历史命令记录*|
|`Ctrl+g`|从执行`Ctrl+r`的搜索历史命令模式中退出*|
|控制快捷键||
|`Ctrl+l`|清除屏幕的所有内容，并在屏幕的最上面开始一个新行，等同于`clear`命令*|
|`Ctrl+s`|锁定终端，使之无法输入内容|
|`Ctrl+q`|解锁执行`Ctrl+s`的锁定状态|
|`Ctrl+z`|暂停执行在终端运行的任务*|
|`！`号开头的快捷键命令||
|`!!`|执行上一条命令|
|`!pw`|执行最近以`pw`开头的命令*|
|`!pw:p`|仅打印最近以`pw`开头的命令，但不执行|
|`!num`|执行历史命令列表的第`num`(数字)命令*|
|`!$`|上一条命令的最后一个参数，相当于`Esc+.(点)`|
|`ESC`相关||
|`Esc+.(点)`|获取上一条命令最后的部分(空格分隔)*|
|`Esc+b`|移动到当前单词的开头|
|`Esc+f`|移动到当前单词的结尾|

## 在 Linux 命令行下查看命令帮助
### 使用 man 获取命令帮助信息
#### man 命令的基本语法
1. `man`命令是`Linux`系统中最核心的命令之一，因为通过它可以查看其他`Linux`命令的使用信息。
2. `man`命令不仅可以查看命令的使用帮助，还可以查看软件服务配置文件、系统调用、库函数等帮助信息。
3. `man`命令功能说明：用于查看命令的帮助信息。
4. `man`命令的参数选项见下表

|数字参数|说明|解释说明|
|--|--|--|
|1|`User Commands`|用户命令相关|
|2|`System Calls`|系统调用相关|
|3|`C Library Functions`|C的库函数相关|
|4|`Devices and Special Files`|设备和特殊文件相关|
|5|`File Formats and Conventions`|文件格式和规则|
|6|`Games et.Al.`|游戏及其他|
|7|`Miscellanea`|宏、包及其他杂项|
|8|`System Administration tools and Deamons`|系统管理员命令和进程|

5. 实践操作
```
[root@oldboy ~]# man cp  #<== 系统管理员常见的用法一般还是直接使用man命令，不带参数。
```
#### 利用 man 查阅命令帮助内容的格式说明
1. 当我们使用`“man命令”`查询命令对应的帮助时，帮助内容中的标题格式所对应的含义具体见下表。

|man 帮助信息中的标题|功能说明(带*的为重点)|
|--|--|
|`NAME`|命令说明及介绍(常见)*|
|`SYNOPSIS`|命令的基本使用语法(常见)*|
|`DESCRIPTION`|命令使用详细描述，以及相关参数选项说明(常见)*<br><br/>有的命令会单独使用参数选项，例如分开介绍`COMMAND LINE OPTIONS`或`OPTIONS`|
|`OPTIONS`|命令相关参数选项说明(有的命令帮助没有此选项)|
|`COMMANDS`|在执行这个程序(软件)的时候，可以在此程序(软件)中执行的命令(不常见)|
|`FILES`|程序涉及(或使用或关联)的相关文件(不常见)|
|`EXAMPLES`|命令的一些例子，这有时很有用*(不常见)|
|`SEE ALSO`|和命令相关的信息说明|
|`BUGS(REPORTING BUGS)`|命令对应缺陷问题的描述|
|`COPYRIGHT`|版权信息相关说明|
|`AUTHOR`|作者介绍|

#### 进入 man 帮助页面中的快捷键功能说明
1. 执行`“man命令”`进入到`man`帮助页面中，实际上就相当于浏览一个文本文件，可以利用下表的快捷键快速查阅想要查找的内容。

|操作键|功能说明|
|--|--|
|`[Page Down]`|向下翻页(也可以空格键替代)|
|`[Page Up]`|向上翻一页|
|`[Home]`|跳转到第一页|
|`[End]`|跳转到最后一页|
|`/oldboy`|向下依次查找`oldboy`字符串，`oldboy`可以替换成你想要搜索的内容|
|`?oldboy`|向上依次查找`oldboy`字符串，`oldboy`可以替换成你想要搜索的内容|
|`n,N`|当使用`“/”`或`“？”`符号向下或向上搜索时，使用`n`会继续当前搜索方向的下一个匹配的查询，使用`N`时则进行相反方向的查询。<br>例如`“/oldboy”`向下搜索后，再按`n`会继续向下搜索`oldboy`，而按`N`就会反向向上搜索`oldboy`了。</br>同理使用`“？oldboy”`向上搜索后，再按`n`会继续向上搜索`oldboy`，而按N就会反向向下搜索`oldboy`了|
|q|结束本次`man`帮助|

#### 使用 --help 参数获取命令帮助信息
1. 除了可以使用`“man命令”`查看命令的帮助信息以外，还可以使用`“命令 --help”`查看命令的使用信息。
2. 中文显示：调整系统字符集`“zh_CN.UTF-8”`。
```
[root@oldboy ~]# cat /etc/sysconfig/i18n
Lang="zh_CN.UTF-8"
[root@oldboy ~]# echo $LANG zh_CN.UTF-8
```
#### 使用 help 命令获取bash内置命令帮助
1. 在`Linux`系统里有一些特殊的命令，他们就是`bash`程序的内置命令，例如`cd`、`history`、`read`等，这些命令在系统目录里就是不存在真实的程序文件(存在于`bash`程序里)，对于这部分命令，查看帮助的方法就是使用`bash`命令，例如：
```
[root@oldboy ~]# help cd
```
2. 如果使用`man cd`，那么通常是查不到帮助信息的，而是会进入`bash`的帮助页面。
#### 使用 info 获取帮助信息
1. `Linux`系统中的`info`命令是一个查看程序对应文档信息的命令，可以作为`man`及`help`命令的帮助补充，不过一般在企业运维工作中，很少会有机会需要使用`info`去查询命令的使用帮助，因此，知道这个命令就好了。
2. 使用`info`命令查看命令帮助的语法操作和`man`类似，示例如下：
```
[root@oldboy ~]# info ls
```
#### 从互联网搜索获取命令帮助信息
1. 除了`Linux`系统自带的帮助功能之外，通过互联网搜索引擎查找命令的帮助信息，可能是很多初学者默认选择的方法，使用互联网搜索引擎查找命令的帮助信息，可能是很多初学者默认选择的方法，但是在逐渐熟悉了`Linux`以后，还是应该养成使用`man`或`help`查看帮助的习惯，这对读者的能力提升极为关键。

## Linux 关机、重启、注销命令
### 重启或关机命令：shutdown
1. `shutdown`是一个用来安全关闭或重启`Linux`系统的命令，系统在关闭之前会通知所有的登录用户，系统即将关闭，此时所有的新用户都不可以登录，与`shutdown`功能类似的命令还有`init`、`halt`、`poweroff`、`reboot`。
2. `shutdown`语法格式
```
shutdown [OPTION]... TIME  [MESSAGE]
shutdown [选项]      时间  消息
```
3. `shutdown`命令和后面的选项之间至少要有一个空格。
4. 通常情况下，我们执行的`shutdown`命令为`shutdown -h now`或`shutdown -r now`。
5. `shutdown`命令的参数说明见下表：

|参数选项|解释说明(带*的为重点)|
|--|--|
|`-r`|重启系统，而不是关机，这个参数在系统重启时经常用到的，例如：`shutdown-r now *`|
|`-h`|关机，这个参数在系统关机时经常用到，例如：`shutdown -h now`|
|`-H`|`关机(halt)`，经过测试，使用这个参数关机后系统并未完全关机，不常用|
|`-P`|`关机(Poweroff)`，不常用|
|`-c`|取消正在执行的`shutdown`指令，极不常用|
|`-k`|只发送关机警告信息并拒绝新用户登录，但是并不实际关机，极不常用|

6. `shutdown`命令的工作过程就是当用户执行了对应参数并附带关机时间的命令之后，通知所有用户即将关机信息，并且在这个时间段禁止新用户登录，仅当到了指定的关机时间时，`shutdown`命令才会根据所接受的参数选项，发送请求给系统的`init`进程，请求将系统调整到对应参数的状态，系统关机状态实际上对应的是`Linux`系统里的运行级别0。
7. 和系统关机相关的运行级别有：`0(关机运行级别)-halt`，`6(重启运行级别)-reboot`，更多相关内容可查看`/etc/inittab`文件。
8. 一分钟后关闭`Linux`系统的命令如下：
```
[root@oldboy ~]# shutdown -h +1           #<==一分钟后关闭Linux系统。
Broadcast message from root@oldboy        #<==通知所有用户关机信息。
        （/dev/pts/1) at 10:26 ...
The system is going down for halt in 1 minute  #<==关机形式及时间提示。
^Cshutdown: Shutdown cancelled                 #<==按Ctrl+c快捷键取消
```
9. 其中，结尾的“+1”表示的是关机时间段，即1分钟后，当然也可以改为五分钟后，这个时间段是以当下系统时间为准来计算的，时间段也可以改为具体的时间点。
10. `shutdown`命令的工作原理为：一旦到达关机时间，`shutdown`命令就会发送请求给系统的init进行将系统调整到合适的运行级别(运行级别命令请参考`runlevel`命令，运行级别请查看`/etc/inittab`文件说明)，其中0表示关机，6表示重启。所以，执行`“init 0”`就表示关机，执行`“init 6”`就表示重启。
11. 11点整重启`Linux`系统的命令如下：
```
[root@oldboy ~]# shutdown -r 11:00
Broadcast message from root@oldboy        
        （/dev/pts/1) at 10:31 ...
The system is going down for reboot in 29 minute!
^Cshutdown: Shutdown cancelled 
```
12. 其中，结尾的11:00表示的是关机的时间点。本命令相当于在11:00的时候告诉`init`进程把运行级别调整为6，即相当于执行`“init 6”`的命令。
13. 立即关闭`Linux`系统的命令如下：
```
[root@oldboy ~]# shutdown -h now
```

### 关机与重启命令：half/poweroff/reboot
1. 从`RedHat`或`CentOS 6`开始，你会发现`halt`、`poweroff`、`reboot`这三个命令对应的都是同一个`man`帮助文档，而`halt`和`poweroff`命令是`reboot`命令的链接文件，因此本书也把这三个命令放在一起讲解。
2. 语法格式如下：
```
reboot [OPTION]...
halt [OPTION]...
poweroff [OPTION]...
```
3. 注意，命令和后面的选项之间至少要有一个空格。通常情况下，我们执行这三个命令时都不带任何参数。
4. 使用`halt`关机的命令如下：
```
[root@oldboy ~]# halt
Broadcast message from root@oldboy        
        （/dev/tty1) at 11:10 ...
The system is going down for halt NOW!
```
5. `halt`命令是`reboot`命令的链接文件，具体查看命令如下：
```
[root@oldboy ~]# ls -l /sbin/halt
lrwxrwxrwx. 1 root root 6 3月   4 2016 /sbin/halt -> reboot
```
6. 使用`poweroff`关机的命令如下：
```
[root@oldboy ~]# poweroff
[root@oldboy ~]# 
Broadcast message from root@oldgirl
        （/dev/pts/0) at 11:21 ...
The system is going down for power off NOW!
```
7. `poweroff`命令也是`reboot`命令的链接文件，具体查看命令如下：
```
[root@oldboy ~]# ll /sbin/poweroff
lrwxrwxrwx. 1 root root 6 3月   4 2016 /sbin/poweroff -> reboot
```
8. 使用`reboot`重启系统命令如下：
```
[root@oldboy ~]# reboot
[root@oldboy ~]# 
Broadcast message from root@oldgirl
        （/dev/pts/0) at 11:24 ...
The system is going down for reboot NOW!
```

### 关机、重启和注销的命令列表
1. 本章在结尾为大家总结了`Linux`下常见的关机、重启、注销等命令，并标注了企业中常用的命令，具体见下表。

|命令|说明|
|--|--|
|关机命令||
|`shutdown -h now`|立刻关机(生产常用)|
|`shutdown -h +1`|1分钟以后关机，1可以是别的数字或时间点，例如：11:00|
|`halt`|立即停止系统，需要人工关闭电源，是`reboot`的链接文件|
|`init 0`|切换运行级别到0，0表示关机，因此此命令的作用就是关机|
|`poweroff`|立即停止系统，并且关闭电源|
|重启命令||
|`reboot`|立即重启(生产常用)|
|`shutdown -r now`|立即重启(生产常用)|
|`shutdown -r +1`|1分钟以后重启|
|`init 6`|切换运行级别到6，6表示重启，因此此命令的作用就是重启|
|注销命令||
|`logout`|注销退出当前用户窗口|
|`exit`|注销退出当前用户窗口，快捷键`Ctrl+d`|


