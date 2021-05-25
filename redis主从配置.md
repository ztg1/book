## 第一步：准备两台linux服务器

第一台服务器：192.168.204.129（主）
第二台服务器：192.168.204.128（从）

## 第二步：配置主服务器

**redis安装自己百度**

   我之前用lnmp安装环境了都已经把redis安装好了

**2.1 修改redis配置文件**

cd /usr/local/redis/etc/

cp redis.conf  redis_old.conf  (配备之前的配置文件)



vi redis.conf



把127.0.0.1改为主服务器的ip 或者0.0.0.0

![image-20200514173804997](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514173804997.png)



把no改为yes。代表开启守护进程模式。在该模式下，redis会在后台运行，并将进程pid号写入至配置文件选项pidfile设置的文件中，此时redis将一直运行，除非手动kill该进程

![image-20200514173849321](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514173849321.png)

把./改为/(根目录)，这是redis数据备份文件dump.rdb存放的路径（可以不更改）

![image-20200514173945871](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514173945871.png)



从节点连接主机的密码123456    

  ![image-20200514174041733](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514174041733.png)



网上说的一写启动配置了解一下（了解一下）

![image-20200514174223761](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514174223761.png)



**2.2 启动redis**
/etc/ini.d/redis restart  重启

要是出现 /var/run/redis.pid  没有什么的

ps -ef|grep redis（查看redis的进程）

把redis 进程杀死，删除/var/run/redis.pid

然后在 /etc/ini.d/redis start 启动就可以



登录主服务器redis客户端，下图可以正常访问

![image-20200514174603215](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514174603215.png)

也可以：

  ![image-20200514174644087](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514174644087.png)



ps -ef|grep redis（查看redis的进程）

![image-20200514174718909](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514174718909.png)

## 第三步：配置从服务器

3.1准备redis的安装包，将安装包放到服务器上

vi redis.conf
把127.0.0.1改为从服务器的ip

![image-20200514174916389](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514174916389.png)



将no改为yes

![image-20200514174934923](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514174934923.png)



添加访问主机的密码masterauth 123456

![image-20200514175006251](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514175006251.png)



添加主机的ip和端口号replicaof 192.168.137.89 6379

![image-20200514175106835](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514175106835.png)

配置了replicaof才会生效

![image-20200514175126652](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514175126652.png)

登录从服务器redis客户端，下图可以正常访问

![image-20200514175226715](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514175226715.png)

第四步：测试
4.1 登录主服务器redis客户端
主机设置键值对aa aa

![image-20200514175257218](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514175257218.png)

4.2 登录从服务器redis客户端
从机获取aa

![image-20200514175338298](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200514175338298.png)

测试结果：成功！！




参考地址：https://blog.csdn.net/wangdongm123/article/details/103818940