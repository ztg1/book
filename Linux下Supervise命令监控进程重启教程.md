


## Linux下Supervise命令监控进程重启教程

### 1、安装Daemontools

```
# for CentOS 7.2 and Ubuntu 16.04
root@vm01:~# wget http://cr.yp.to/daemontools/daemontools-0.76.tar.gz
......
root@vm01:~#

# for MacOS
# curl -o daemontools-0.76.tar.gz http://cr.yp.to/daemontools/daemontools-0.76.tar.gz
```

 ### 2、解压并修改文件

```
root@vm01:~# tar xvzf daemontools-0.76.tar.gz
......
root@vm01:~# cd admin/daemontools-0.76
root@vm01:~/admin/daemontools-0.76#
```

### 3、编辑conf-cc文件，在conf-cc文件最后加上“-include /usr/include/errno.h ”

```
root@vm01:~/admin/daemontools-0.76# vi src/conf-cc
gcc -O2 -Wimplicit -Wunused -Wcomment -Wchar-subscripts -Wuninitialized -Wshadow -Wcast-qual -Wcast-align -Wwrite-str
ings -include /usr/include/errno.h 

This will be used to compile .c files.
root@vm01:~/admin/daemontools-0.76# 
```

### 4、执行安装

```
root@vm01:~/admin/daemontools-0.76# pwd
/root/admin/daemontools-0.76
root@vm01:~/admin/daemontools-0.76# sudo package/install
Linking ./src/* into ./compile...
Compiling everything in ./compile...
sh find-systype.sh > systype
rm -f compile
sh print-cc.sh > compile
chmod 555 compile
./compile byte_chr.c
./compile byte_copy.c
./compile byte_cr.c
./compile byte_diff.c
./compile byte_rchr.c
./compile fmt_uint.c
./compile fmt_uint0.c
......
Copying commands into ./command...
Creating symlink daemontools -> daemontools-0.76...
Making command links in /command...
Making compatibility links in /usr/local/bin...
Creating /service...
Adding svscanboot to /etc/rc.local...
Reboot now to start svscan.
root@vm01:~/admin/daemontools-0.76#
```

### 5、检查安装

```
# for Ubuntu 16.04 有svscan、supervise等命令就表示安装成功
root@vm01:~/admin/daemontools# ls /usr/local/bin
chardetect       cloud-init-per    envuidgid    markdown_py  pip2.7         supervise   svstat
cheetah          easy_install      fghack       multilog     readproctitle  svc         tai64n
cheetah-analyze  easy_install-2.7  jsondiff     pgrphack     setlock        svok        tai64nlocal
cheetah-compile  easy_install-3.6  jsonpatch    pip          setuidgid      svscan      wheel
cloud-init       envdir            jsonpointer  pip2         softlimit      svscanboot
root@vm01:~/admin/daemontools# ls -la /command
total 8
drwxr-xr-x  2 root root 4096 Jul 13 14:56 .
drwxr-xr-x 24 root root 4096 Jul 13 14:56 ..
lrwxrwxrwx  1 root root   38 Jul 13 14:56 envdir -> /root/admin/daemontools/command/envdir
lrwxrwxrwx  1 root root   41 Jul 13 14:56 envuidgid -> /root/admin/daemontools/command/envuidgid
lrwxrwxrwx  1 root root   38 Jul 13 14:56 fghack -> /root/admin/daemontools/command/fghack
lrwxrwxrwx  1 root root   40 Jul 13 14:56 multilog -> /root/admin/daemontools/command/multilog
lrwxrwxrwx  1 root root   40 Jul 13 14:56 pgrphack -> /root/admin/daemontools/command/pgrphack
lrwxrwxrwx  1 root root   45 Jul 13 14:56 readproctitle -> /root/admin/daemontools/command/readproctitle
lrwxrwxrwx  1 root root   39 Jul 13 14:56 setlock -> /root/admin/daemontools/command/setlock
lrwxrwxrwx  1 root root   41 Jul 13 14:56 setuidgid -> /root/admin/daemontools/command/setuidgid
lrwxrwxrwx  1 root root   41 Jul 13 14:56 softlimit -> /root/admin/daemontools/command/softlimit
lrwxrwxrwx  1 root root   41 Jul 13 14:56 supervise -> /root/admin/daemontools/command/supervise
lrwxrwxrwx  1 root root   35 Jul 13 14:56 svc -> /root/admin/daemontools/command/svc
lrwxrwxrwx  1 root root   36 Jul 13 14:56 svok -> /root/admin/daemontools/command/svok
lrwxrwxrwx  1 root root   38 Jul 13 14:56 svscan -> /root/admin/daemontools/command/svscan
lrwxrwxrwx  1 root root   42 Jul 13 14:56 svscanboot -> /root/admin/daemontools/command/svscanboot
lrwxrwxrwx  1 root root   38 Jul 13 14:56 svstat -> /root/admin/daemontools/command/svstat
lrwxrwxrwx  1 root root   38 Jul 13 14:56 tai64n -> /root/admin/daemontools/command/tai64n
lrwxrwxrwx  1 root root   43 Jul 13 14:56 tai64nlocal -> /root/admin/daemontools/command/tai64nlocal
root@vm01:~/admin/daemontools# 
```

```
# for CentOS 7.2 有最后一行就表示安装成功
[root@gamesrv bin]# more /etc/inittab
# inittab is no longer used when using systemd.
#
# ADDING CONFIGURATION HERE WILL HAVE NO EFFECT ON YOUR SYSTEM.
#
# Ctrl-Alt-Delete is handled by /usr/lib/systemd/system/ctrl-alt-del.target
#
# systemd uses 'targets' instead of runlevels. By default, there are two main targets:
#
# multi-user.target: analogous to runlevel 3
# graphical.target: analogous to runlevel 5
#
# To view current default target, run:
# systemctl get-default
#
# To set a default target, run:
# systemctl set-default TARGET.target
#

SV:123456:respawn:/command/svscanboot
[root@gamesrv bin]# 
```

### 6、配置run文件

```
root@vm01:~# cd /root/leafserver/bin
root@vm01:~/leafserver/bin# vi run
#!/bin/bash

cd /root/leafserver/bin

./server
root@vm01:~/leafserver/bin# chmod u+x run
root@vm01:~/leafserver/bin#
```

### 7、配置supervise启动、停止及监控脚本

```
#配置启动脚本
root@vm01:~/leafserver/bin# vi startSupervise.sh 
#!/bin/bash

supervise /root/leafserver/bin/ >gamesrv-`date +'%Y%m%d-%H%M%S'`.log 2>&1 &
root@vm01:~/leafserver/bin# chmod u+x startSupervise.sh
root@vm01:~/leafserver/bin#

#配置停止脚本
root@vm01:~/leafserver/bin# vi 01_killSupervise.sh 
#!/bin/bash

PIDS=`ps -ef |grep supervise |grep -v grep | awk '{print $2}'`
if [ "$PIDS" != "" ]; then
	kill -9 $PIDS
	echo `date +%F" "%H:%M:%S` "Supervise has been KILLed!"
else
	echo `date +%F" "%H:%M:%S` "Supervise is NOT runing!"
fi

root@vm01:~/leafserver/bin# vi 02_stopSrv.sh 
#!/bin/bash

PIDS=`ps -ef |grep /server |grep -v grep | awk '{print $2}'`
if [ "$PIDS" != "" ]; then
	kill -9 $PIDS
	echo `date +%F" "%H:%M:%S` "Game Server has been KILLed!"
else
	echo `date +%F" "%H:%M:%S` "Game Server is NOT runing!"
fi
root@vm01:~/leafserver/bin# vi monitorSrv.sh 
#!/bin/bash

PIDS=`ps -ef |grep supervise |grep -v grep | awk '{print $2}'`
if [ "$PIDS" != "" ]; then
        echo `date +%F" "%H:%M:%S` "Supervise is runing!"
else
        echo `date +%F" "%H:%M:%S` "Supervise is NOT runing!"

fi


PIDS=`ps -ef |grep /server |grep -v grep | awk '{print $2}'`
if [ "$PIDS" != "" ]; then
        echo `date +%F" "%H:%M:%S` "Game Server is runing!"
else
        echo `date +%F" "%H:%M:%S` "Game Server is NOT runing!"

fi
root@vm01:~/leafserver/bin# chmod u+x 01_killSupervise.sh 02_stopSrv.sh monitorSrv.sh 
root@vm01:~/leafserver/bin# 

```

### 8、启动游戏服务

```
root@vm01:~/leafserver/bin# ./startSupervise.sh
#观察日志是否正常
root@vm01:~/leafserver/bin# tail gamesrv-2019-713-144144.log
......
```



### 9、停止游戏服务

```
# 由于受到supervise的监控，要完全停止掉游戏进程，必须先停止掉supervise，再停止游戏的进程即可。
root@vm01:~/leafserver/bin# ./01_killSupervise.sh
root@vm01:~/leafserver/bin# ./02_stopSrv.sh
```

