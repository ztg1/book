# Box配置笔记





### 1、大体结构图

![image-20210421100206492](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210421100206492.png)

### 2、Box配置IP

   用网线或者USB线连接盒子，然后FlexManager客户端，配置工具配置

![image-20210421100632302](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210421100632302.png)

![image-20210421100659505](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210421100659505.png)





扫描,读取配置，最后配置盒子IP。



### 3、远程数据下载配置

​     

   一种是 Modbus 配置 （设备接线是485）

![image-20210421100959507](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210421100959507.png)

二种是 以太网线

![image-20210421101321193](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210421101321193.png)



第三种mqtt配置

![image-20210421101616670](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210421101616670.png)

![image-20210421101639689](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210421101639689.png)





### 4、点位配置

 按照文档配置即可







## 5、主从配置记录

   模块机就是一主多重，他们怎么连接线我机不管，大概就是，没有机组都有自己的地址，点位也有地址

![image-20210421102054074](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210421102054074.png)

 命令的模式大体就是

 主地址：从地址：点位地址：........

下面的配置

![image-20210421102522035](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20210421102522035.png)